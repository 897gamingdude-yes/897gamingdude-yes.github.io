<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Jaeger Pilot VR - Combat Edition</title>
    <script src="https://aframe.io/releases/1.4.2/aframe.min.js"></script>
    <script src="https://unpkg.com/aframe-environment-component@1.3.2/dist/aframe-environment-component.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/c-frame/aframe-physics-system@v4.2.2/dist/aframe-physics-system.min.js"></script>
    
    <script>
      // Component to handle the Kaiju "Explosion"/Hit effect
      AFRAME.registerComponent('kaiju-target', {
        init: function () {
          this.el.addEventListener('collisestart', (e) => {
            this.el.setAttribute('material', 'color', 'yellow');
            setTimeout(() => {
              this.el.setAttribute('material', 'color', '#770000');
              // Teleport Kaiju to a new spot to "reset" the fight
              this.el.setAttribute('position', {x: (Math.random() - 0.5) * 40, y: 20, z: -60});
            }, 500);
          });
        }
      });

      // Simple Movement Component for Oculus Joystick
      AFRAME.registerComponent('thumbstick-logging', {
        init: function () {
          this.el.addEventListener('thumbstickmoved', (evt) => {
            let rig = document.querySelector('#rig');
            let pos = rig.getAttribute('position');
            // Move the giant robot based on joystick Y axis
            if (evt.detail.y > 0.95) { pos.z += 0.5; }
            if (evt.detail.y < -0.95) { pos.z -= 0.5; }
            rig.setAttribute('position', pos);
          });
        }
      });
    </script>
  </head>
  <body>
    <a-scene physics="debug: false; gravity: 0">
      
      <a-assets>
        <a-mixin id="giant-hand" 
                 geometry="primitive: box; width: 4; height: 2; depth: 4" 
                 material="color: #555; metalness: 0.8"
                 static-body></a-mixin>
      </a-assets>

      <a-entity environment="preset: arches; groundColor: #000; grid: cross"></a-entity>

      <a-entity id="rig" position="0 30 0">
        <a-camera></a-camera>
        
        <a-entity oculus-touch-controls="hand: left" thumbstick-logging>
            <a-entity mixin="giant-hand"></a-entity>
        </a-entity>

        <a-entity oculus-touch-controls="hand: right">
            <a-entity mixin="giant-hand"></a-entity>
        </a-entity>
      </a-entity>

      <a-entity id="kaiju" 
                kaiju-target
                geometry="primitive: box; width: 10; height: 50; depth: 10" 
                material="color: #770000" 
                position="0 25 -50"
                static-body>
      </a-entity>

    </a-scene>
  </body>
</html>
