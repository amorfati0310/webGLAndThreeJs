## ThreeJS

중요한 것 세가지 씬, 카메라 , 렌더러

렌더러로 보통 window.innerWidth, window.innerHeight를 가지고 온다
화면 비율에 맞추기

카메라는 주로 perspectiveCamera를 사용 !
여기서 첫번쨰 속성은 시야각 , 두번째는 가로/세로 apspectRatio
나머지 두가지 속성은 clipping plane의 near /far값입니다.

물체가 카메로 far보다 멀거나 near보다 가까울 때는 render되지 않습니다.


webGlRedner를 사용하여 그림

```js
  var scene = new THREE.Scene();
  var camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

  var renderer = new THREE.WebGLRenderer();
  renderer.setSize( window.innerWidth, window.innerHeight );
  document.body.appendChild( renderer.domElement );
```


큐브 만들기

큐브 만들 떄 필요한 친구들은 Geometry, material, cube
면에 필요한 Geometry , material어떻게 칠할건지
Mesh는 (Geometry, material)을 가지고 조합해서 만든 인스턴스

이것을 씬에 추가해줍니다. scene.add(cube)  // 0,0,0 에 위치하게 됨

Scene 렌더링
아직 렌더링을 안해서 아무것도 보이지가 않을 것입니다.
렌더링 하는 function을 아래와 같이 만들어 줍니다. 초당 60번 그려줍니다.

requerstAnimationFram 의 장점중 하나는
사용자가 다른 tap을 작업하고 있을 때는 그리지 않습니다

```javascript
  var geometry = new THREE.BoxGeometry( 1, 1, 1 );
  var material = new THREE.MeshBasicMaterial( { color: 0x74c0fc } );
  var cube = new THREE.Mesh( geometry, material );
  scene.add( cube );

  camera.position.z = 5;

  function render() {
    requestAnimationFrame( render );
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
    renderer.render( scene, camera );
  }
  render();
```

구를 추가해보자

```
  var sphereGeometry = new THREE.SphereGeometry(4,32,32);
  var sphereMeterial = new THREE.MeshBasicMaterial({color: 0xFE98A0});
  var sphere = new THREE.Mesh(sphereGeometry, sphereMeterial);
  sphere.position.x = -15;
  sphere.position.y = 2;
  sphere.position.z = 0;
  scene.add(sphere);

```
