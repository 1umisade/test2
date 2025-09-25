

# Proton


## Structure
<img src="images/proton.png" height="300">

<details style="display:inline;">
  <summary style="display:inline; cursor:pointer;">View structure source 🔎</summary>
  <p>
    <a href="https://pubchem.ncbi.nlm.nih.gov/compound/Proton" target="_blank">
    https://pubchem.ncbi.nlm.nih.gov/compound/Proton
    </a>
  </p> 
  <img src="" height="300">
</details><br><br><br><br>



## function
<span>
<img src="images/Screenshot 2025-09-04 092155.png" height="600"><br>
<img src="images/proton_collision_layer.png" height="300"><br>
 <small>Proton node setup</small><br><br>
  Proton is a positively charged particle that makes up the nuclei of atoms together with neutrally charged neutrons. 
   <details style="display:inline;">
    <summary style="display:inline; cursor:pointer;">🔎</summary>
    <img src="Screenshot 2025-09-04 100641.png" height="250"><br>
    <small>Source: Wikipedia (https://en.wikipedia.org/wiki/Atom) </small>





  </details>
Protons play a central role in photosynthesis where they are created inside the lumen with the oxidation of water.
   <details style="display:inline;">
    <summary style="display:inline; cursor:pointer;">🔎</summary>
    <img src="images/Screenshot 2025-09-04 100053.png" height="250"><br>
    <small>Source: Plant physiology and development (7th edition) (page 264)</small>




  </details>
Protons then flow through ATP-synthase which enables the enzyme to create ATP.
   <details style="display:inline;">
    <summary style="display:inline; cursor:pointer;">🔎</summary>
    <img src="images/Screenshot 2025-09-04 095758.png" height="250"><br>
    <small>Source: Plant physiology and development (7th edition) (page 272)</small><br>
  </details> 
<br><br>


   <details style="display:inline;">
    <summary style="display:inline; cursor:pointer;">View proton's script🔎</summary>

      extends CharacterBody2D
      
      var speed = 125
      var direction = Vector2(-1, -1)
      var rotation_speed = 2
      var rotation_direction = -1

      func _movement(delta):
        velocity = speed * direction
        rotation = rotation + (delta * rotation_speed * rotation_direction)
        var collision = move_and_collide(velocity * delta)
        if collision:
          var normal = collision.get_normal()
          direction = direction.bounce(normal).normalized()
          position = position - (velocity.normalized() * 0.0)
          rotation_direction = rotation_direction * (-1)

      func _ready():
        add_to_group("proton")

      func _physics_process(delta):
        _movement(delta)

  </details> 
<br><br><br>

  Known issues<br>
  • Proton speed is arbitrary





