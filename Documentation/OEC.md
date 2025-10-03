extends CharacterBody2D

## Ferredoxin–NADP+ Reductase (FNR)


## Variables

# Movement
var speed = 250
var direction = Vector2(-1, -1)
var rotation_speed = 0
var rotation_direction = -1

# Pulling & docking
const LOCKING_LERP = 0.08  ## NEW
var NADPs_that_are_pulled_towards_FNR_center: Array = []      
var ferredoxins_that_are_pulled_towards_FNR_center: Array = [] 

var NADPs_inside_FNR_center: Array = []                     
var ferredoxins_inside_FNR_center: Array = []             

## keys for the nested dictionaries
const KEY_NADP := "distance_of_bound_NADP_to_FNR_center"      
const KEY_FDX  := "distance_of_bound_ferredoxin_to_FNR_center"     

var dictionary_for_distances := {                                  
	KEY_NADP: Dictionary(),   ## Node2D (NADP)      -> Vector2 offset from $Center
	KEY_FDX:  Dictionary()    ## Node2D (ferredoxin)-> Vector2 offset from $Center
}




## Triggered functions

func when_body_enters_FNR_center(body: Node2D) -> void:
	if body.is_in_group("NADP+") \
	and body.NADP_is_electronised == false \
	and NADPs_inside_FNR_center.is_empty():
		var NADP = body
		NADP.get_node_or_null("CollisionShape2D").set_deferred("disabled", true)
		NADP.set_physics_process(false)
		NADPs_inside_FNR_center.append(NADP)
		dictionary_for_distances[KEY_NADP][NADP] = NADP.global_position - $Center.global_position
		await get_tree().create_timer(0.01).timeout
		var CollisionShape_copy
		CollisionShape_copy = CollisionShape2D.new()
		CollisionShape_copy.shape = NADP.get_node_or_null("CollisionShape2D").shape
		add_child(CollisionShape_copy)
		CollisionShape_copy.global_transform = NADP.get_node_or_null("CollisionShape2D").global_transform
		$"../ferredoxin".releasing_of_electrons_from_ferredoxin()  ## this is the only difference between if statements. try combining
		
		await get_tree().create_timer(5).timeout
		self.get_node_or_null("Center").set_deferred("monitoring", false)
		self.get_node_or_null("Pulling_area").set_deferred("monitoring", false)
		NADP.set_physics_process(true)
		dictionary_for_distances[KEY_NADP].erase(NADP)
		CollisionShape_copy.queue_free()
		NADPs_inside_FNR_center.clear()
		NADP.get_node_or_null("CollisionShape2D").set_deferred("disabled", false)
		
		await get_tree().create_timer(5).timeout
		self.get_node_or_null("Center").set_deferred("monitoring", true)
		self.get_node_or_null("Pulling_area").set_deferred("monitoring", true)




	elif body.is_in_group("ferredoxin") \
	and ferredoxins_inside_FNR_center.is_empty():
		var ferredoxin = body
		ferredoxin.get_node_or_null("CollisionShape2D").set_deferred("disabled", true)
		ferredoxin.set_physics_process(false)
		ferredoxins_inside_FNR_center.append(ferredoxin)
		dictionary_for_distances[KEY_FDX][ferredoxin] = ferredoxin.global_position - $Center.global_position
		await get_tree().create_timer(0.01).timeout
		var CollisionShape_copy
		CollisionShape_copy = CollisionShape2D.new()
		CollisionShape_copy.shape = ferredoxin.get_node_or_null("CollisionShape2D").shape
		add_child(CollisionShape_copy)
		CollisionShape_copy.global_transform = ferredoxin.get_node_or_null("CollisionShape2D").global_transform ## try using offset vector instead
		ferredoxin.releasing_of_electrons_from_ferredoxin()
		
		await get_tree().create_timer(5).timeout
		self.get_node_or_null("Center").set_deferred("monitoring", false)
		self.get_node_or_null("Pulling_area").set_deferred("monitoring", false)
		ferredoxin.set_physics_process(true)
		dictionary_for_distances[KEY_FDX].erase(ferredoxin)
		CollisionShape_copy.queue_free()
		ferredoxins_inside_FNR_center.clear()
		ferredoxin.get_node_or_null("CollisionShape2D").set_deferred("disabled", false)
		
		await get_tree().create_timer(5).timeout
		self.get_node_or_null("Center").set_deferred("monitoring", true)
		self.get_node_or_null("Pulling_area").set_deferred("monitoring", true)











func when_body_enters_pulling_area(body) -> void:
	if body.is_in_group("NADP+") \
	and NADPs_that_are_pulled_towards_FNR_center.size() < 1:
		NADPs_that_are_pulled_towards_FNR_center.append(body)
		await get_tree().create_timer(1).timeout
		NADPs_that_are_pulled_towards_FNR_center.erase(body)

	elif body.is_in_group("ferredoxin") \
	and ferredoxins_that_are_pulled_towards_FNR_center.size() < 1:
		ferredoxins_that_are_pulled_towards_FNR_center.append(body)
		await get_tree().create_timer(1).timeout
		ferredoxins_that_are_pulled_towards_FNR_center.erase(body)


## FIRST frame 

func connect_body_entered_FNR_center() -> void:
	$Center.body_entered.connect(when_body_enters_FNR_center)

func connect_body_entered_pulling_area() -> void:
	$Pulling_area.body_entered.connect(when_body_enters_pulling_area)

func connect_body_exited_pulling_area() -> void:
	$Pulling_area.body_exited.connect(func(body):
		NADPs_that_are_pulled_towards_FNR_center.erase(body)
		ferredoxins_that_are_pulled_towards_FNR_center.erase(body)
	)


## EVERY frame

func pulling_towards_reaction_center() -> void:
	for body in NADPs_that_are_pulled_towards_FNR_center + ferredoxins_that_are_pulled_towards_FNR_center:
		if body.is_in_group("NADP+") or body.is_in_group("ferredoxin"):
			const LERP_STRENGTH := 0.2
			var target_direction = ($Pulling_area.global_position - body.global_position).normalized()
			if "direction" in body:
				body.direction = body.direction.lerp(target_direction, LERP_STRENGTH).normalized()


func _lerping_locked_particles_of_FNR() -> void:  ## NEW
	for body in dictionary_for_distances[KEY_NADP].keys():
		var offset = dictionary_for_distances[KEY_NADP][body]
		#var target_offset = offset.lerp(Vector2(0,0), LOCKING_LERP)
		#dictionary_for_distances[KEY_NADP][body] = target_offset
		body.global_position = $Center.global_position + offset
	for body in dictionary_for_distances[KEY_FDX].keys():
		var offset = dictionary_for_distances[KEY_FDX][body]
		#var target_offset = offset.lerp(Vector2(0,0), LOCKING_LERP)
		#dictionary_for_distances[KEY_FDX][body] = target_offset
		body.global_position = $Center.global_position + offset



func _ready():
	add_to_group("FNR")
	connect_body_entered_FNR_center()
	connect_body_entered_pulling_area()
	connect_body_exited_pulling_area()


func _physics_process(delta: float) -> void:
	velocity = speed * direction
	var collision := move_and_collide(velocity * delta)
	if collision:
		var normal := collision.get_normal()
		direction = direction.bounce(normal).normalized()
		position = position - (velocity.normalized() * 0.5)
		rotation_direction *= -1
	#shifting()
	pulling_towards_reaction_center()
	_lerping_locked_particles_of_FNR() 





#extends CharacterBody2D
#
### Ferredoxin–NADP+ Reductase (FNR)
#
#
### Variables
#
## Movement
#var speed = 250
#var direction = Vector2(-1, -1)
#var rotation_speed = 0
#var rotation_direction = -1
#
## Pulling & docking
#const LOCKING_LERP = 0.08  ## NEW
#var NADPs_that_are_pulled_towards_FNR_center: Array = []      
#var ferredoxins_that_are_pulled_towards_FNR_center: Array = [] 
#
#var NADPs_inside_FNR_center: Array = []                     
#var ferredoxins_inside_FNR_center: Array = []        
#
#var locked_NADP: Node2D = null
#var locked_NADP_offset := Vector2.ZERO
#
#var locked_ferredoxin: Node2D = null
#var locked_ferredoxin_offset := Vector2.ZERO     
#
#### keys for the nested dictionaries
##const KEY_NADP := "distance_of_bound_NADP_to_FNR_center"      
##const KEY_FDX  := "distance_of_bound_ferredoxin_to_FNR_center"     
##
##var dictionary_for_distances := {                                  
	##KEY_NADP: Dictionary(),   ## Node2D (NADP)      -> Vector2 offset from $Center
	##KEY_FDX:  Dictionary()    ## Node2D (ferredoxin)-> Vector2 offset from $Center
##}
#
#
#
#
### Triggered functions
#
#func when_body_enters_FNR_center(body: Node2D) -> void:
	#if body.is_in_group("NADP+") \
	#and body.NADP_is_electronised == false \
	#and NADPs_inside_FNR_center.is_empty():
		#var locked_NADP = body
		#locked_NADP.get_node_or_null("CollisionShape2D").set_deferred("disabled", true)
		#locked_NADP.set_physics_process(false)
		#NADPs_inside_FNR_center.append(locked_NADP)
		#locked_NADP_offset = locked_NADP.global_position - $Center.global_position
		#await get_tree().create_timer(0.01).timeout
		#var CollisionShape_copy
		#CollisionShape_copy = CollisionShape2D.new()
		#CollisionShape_copy.shape = locked_NADP.get_node_or_null("CollisionShape2D").shape
		#add_child(CollisionShape_copy)
		#CollisionShape_copy.global_transform = locked_NADP.get_node_or_null("CollisionShape2D").global_transform
		#$"../ferredoxin".releasing_of_electrons_from_ferredoxin()
		#
		#await get_tree().create_timer(5).timeout
		#self.get_node_or_null("Center").set_deferred("monitoring", false)
		#self.get_node_or_null("Pulling_area").set_deferred("monitoring", false)
		#locked_NADP.set_physics_process(true)
		#CollisionShape_copy.queue_free()
		#NADPs_inside_FNR_center.clear()
		#locked_NADP.get_node_or_null("CollisionShape2D").set_deferred("disabled", false)
		#
		#await get_tree().create_timer(5).timeout
		#self.get_node_or_null("Center").set_deferred("monitoring", true)
		#self.get_node_or_null("Pulling_area").set_deferred("monitoring", true)
#
#
#
#
	#elif body.is_in_group("ferredoxin") \
	#and ferredoxins_inside_FNR_center.is_empty():
		#var locked_ferredoxin = body
		#locked_ferredoxin.get_node_or_null("CollisionShape2D").set_deferred("disabled", true)
		#locked_ferredoxin.set_physics_process(false)
		#ferredoxins_inside_FNR_center.append(locked_ferredoxin)
		#locked_ferredoxin_offset = locked_ferredoxin.global_position - $Center.global_position
		#await get_tree().create_timer(0.01).timeout
		#var CollisionShape_copy
		#CollisionShape_copy = CollisionShape2D.new()
		#CollisionShape_copy.shape = locked_ferredoxin.get_node_or_null("CollisionShape2D").shape
		#add_child(CollisionShape_copy)
		#CollisionShape_copy.global_transform = locked_ferredoxin.get_node_or_null("CollisionShape2D").global_transform
		#locked_ferredoxin.releasing_of_electrons_from_ferredoxin()
		#
		#await get_tree().create_timer(5).timeout
		#self.get_node_or_null("Center").set_deferred("monitoring", false)
		#self.get_node_or_null("Pulling_area").set_deferred("monitoring", false)
		#locked_ferredoxin.set_physics_process(true)
		#CollisionShape_copy.queue_free()
		#ferredoxins_inside_FNR_center.clear()
		#locked_ferredoxin.get_node_or_null("CollisionShape2D").set_deferred("disabled", false)
		#
		#await get_tree().create_timer(5).timeout
		#self.get_node_or_null("Center").set_deferred("monitoring", true)
		#self.get_node_or_null("Pulling_area").set_deferred("monitoring", true)
#
#
#
#
#
#
#
#
#
#
#
#func when_body_enters_pulling_area(body) -> void:
	#if body.is_in_group("NADP+") \
	#and NADPs_that_are_pulled_towards_FNR_center.size() < 1:
		#NADPs_that_are_pulled_towards_FNR_center.append(body)
		#await get_tree().create_timer(1).timeout
		#NADPs_that_are_pulled_towards_FNR_center.erase(body)
#
	#elif body.is_in_group("ferredoxin") \
	#and ferredoxins_that_are_pulled_towards_FNR_center.size() < 1:
		#ferredoxins_that_are_pulled_towards_FNR_center.append(body)
		#await get_tree().create_timer(1).timeout
		#ferredoxins_that_are_pulled_towards_FNR_center.erase(body)
#
#
### FIRST frame 
#
#func connect_body_entered_FNR_center() -> void:
	#$Center.body_entered.connect(when_body_enters_FNR_center)
#
#func connect_body_entered_pulling_area() -> void:
	#$Pulling_area.body_entered.connect(when_body_enters_pulling_area)
#
#func connect_body_exited_pulling_area() -> void:
	#$Pulling_area.body_exited.connect(func(body):
		#NADPs_that_are_pulled_towards_FNR_center.erase(body)
		#ferredoxins_that_are_pulled_towards_FNR_center.erase(body)
	#)
#
#
### EVERY frame
#
#func pulling_towards_reaction_center() -> void:
	#for body in NADPs_that_are_pulled_towards_FNR_center + ferredoxins_that_are_pulled_towards_FNR_center:
		#if body.is_in_group("NADP+") or body.is_in_group("ferredoxin"):
			#const LERP_STRENGTH := 0.2
			#var target_direction = ($Pulling_area.global_position - body.global_position).normalized()
			#if "direction" in body:
				#body.direction = body.direction.lerp(target_direction, LERP_STRENGTH).normalized()
#
#
#func _lerping_locked_particles_of_FNR() -> void:  ## NEW
	#if locked_NADP:
		#locked_NADP_offset = locked_NADP_offset.lerp(Vector2.ZERO, LOCKING_LERP)
		#locked_NADP.global_position = $Center.global_position + locked_NADP_offset
	#if locked_ferredoxin:
		#locked_ferredoxin_offset = locked_ferredoxin_offset.lerp(Vector2.ZERO, LOCKING_LERP)
		#locked_ferredoxin.global_position = $Center.global_position + locked_ferredoxin_offset
#
#
#
#func _ready():
	#add_to_group("FNR")
	#connect_body_entered_FNR_center()
	#connect_body_entered_pulling_area()
	#connect_body_exited_pulling_area()
#
#
#func _physics_process(delta: float) -> void:
	#velocity = speed * direction
	#var collision := move_and_collide(velocity * delta)
	#if collision:
		#var normal := collision.get_normal()
		#direction = direction.bounce(normal).normalized()
		#position = position - (velocity.normalized() * 0.5)
		#rotation_direction *= -1
	##shifting()
	#pulling_towards_reaction_center()
	#_lerping_locked_particles_of_FNR() 
