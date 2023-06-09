---
---

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <meta http-equiv="Content-Style-Type" content="text/css">
  <title></title>
  <meta name="Generator" content="Cocoa HTML Writer">
  <meta name="CocoaVersion" content="2113.6">
  <style type="text/css">
    p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Helvetica}
    p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Helvetica; min-height: 14.0px}
  </style>
</head>
<body>
<p class="p1">&lt;!DOCTYPE html&gt;</p>
<p class="p1">&lt;html lang="en"&gt;</p>
<p class="p1">&lt;head&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;meta charset="UTF-8"&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;title&gt;3D Model Viewer&lt;/title&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"&gt;&lt;/script&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;script src="https://threejs.org/examples/js/loaders/OBJLoader.js"&gt;&lt;/script&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;script src="https://threejs.org/examples/js/loaders/MTLLoader.js"&gt;&lt;/script&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;script src="https://threejs.org/examples/js/controls/OrbitControls.js"&gt;&lt;/script&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;style&gt;</p>
<p class="p1"><span class="Apple-converted-space">    </span>body { margin: 0; }</p>
<p class="p1"><span class="Apple-converted-space">    </span>canvas { display: block; }</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;/style&gt;</p>
<p class="p1">&lt;/head&gt;</p>
<p class="p1">&lt;body&gt;</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;script&gt;</p>
<p class="p1"><span class="Apple-converted-space">    </span>// Set up the scene, camera, and renderer</p>
<p class="p1"><span class="Apple-converted-space">    </span>const scene = new THREE.Scene();</p>
<p class="p1"><span class="Apple-converted-space">    </span>const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);</p>
<p class="p1"><span class="Apple-converted-space">    </span>const renderer = new THREE.WebGLRenderer();</p>
<p class="p1"><span class="Apple-converted-space">    </span>renderer.setSize(window.innerWidth, window.innerHeight);</p>
<p class="p1"><span class="Apple-converted-space">    </span>document.body.appendChild(renderer.domElement);</p>
<p class="p2"><br></p>
<p class="p1"><span class="Apple-converted-space">    </span>// Add OrbitControls</p>
<p class="p1"><span class="Apple-converted-space">    </span>const controls = new THREE.OrbitControls(camera, renderer.domElement);</p>
<p class="p1"><span class="Apple-converted-space">    </span>controls.target.set(0, 0, 0);</p>
<p class="p1"><span class="Apple-converted-space">    </span>controls.update();</p>
<p class="p2"><br></p>
<p class="p1"><span class="Apple-converted-space">    </span>// Set up the lights</p>
<p class="p1"><span class="Apple-converted-space">    </span>const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);</p>
<p class="p1"><span class="Apple-converted-space">    </span>scene.add(ambientLight);</p>
<p class="p1"><span class="Apple-converted-space">    </span>const pointLight = new THREE.PointLight(0xffffff, 1);</p>
<p class="p1"><span class="Apple-converted-space">    </span>camera.add(pointLight);</p>
<p class="p1"><span class="Apple-converted-space">    </span>scene.add(camera);</p>
<p class="p2"><br></p>
<p class="p1"><span class="Apple-converted-space">    </span>// Load the materials and the 3D model</p>
<p class="p1"><span class="Apple-converted-space">    </span>const mtlLoader = new THREE.MTLLoader();</p>
<p class="p1"><span class="Apple-converted-space">    </span>mtlLoader.load('https://storage.googleapis.com/drone-mvp-1/MVP1.2%20(Holes%20closed).mtl', materials =&gt; {</p>
<p class="p1"><span class="Apple-converted-space">      </span>materials.preload();</p>
<p class="p1"><span class="Apple-converted-space">      </span>const objLoader = new THREE.OBJLoader();</p>
<p class="p1"><span class="Apple-converted-space">      </span>objLoader.setMaterials(materials);</p>
<p class="p1"><span class="Apple-converted-space">      </span>objLoader.load('https://storage.googleapis.com/drone-mvp-1/MVP1.2%20(Holes%20closed).obj', object =&gt; {</p>
<p class="p1"><span class="Apple-converted-space">        </span>scene.add(object);</p>
<p class="p1"><span class="Apple-converted-space">      </span>});</p>
<p class="p1"><span class="Apple-converted-space">    </span>});</p>
<p class="p2"><br></p>
<p class="p1"><span class="Apple-converted-space">    </span>camera.position.z = 5;</p>
<p class="p2"><br></p>
<p class="p1"><span class="Apple-converted-space">    </span>// Render the scene</p>
<p class="p1"><span class="Apple-converted-space">    </span>const animate = function () {</p>
<p class="p1"><span class="Apple-converted-space">      </span>requestAnimationFrame(animate);</p>
<p class="p1"><span class="Apple-converted-space">      </span>controls.update();</p>
<p class="p1"><span class="Apple-converted-space">      </span>renderer.render(scene, camera);</p>
<p class="p1"><span class="Apple-converted-space">    </span>};</p>
<p class="p2"><br></p>
<p class="p1"><span class="Apple-converted-space">    </span>animate();</p>
<p class="p1"><span class="Apple-converted-space">  </span>&lt;/script&gt;</p>
<p class="p1">&lt;/body&gt;</p>
<p class="p1">&lt;/html&gt;</p>
</body>
</html>
