proctree.js
===========

Procedural tree creation library
    
### Usage ###
	
#### GLGE

Mesh creation, [GLGE](https://github.com/supereggbert/GLGE) example:
```html
<script>
	var myTree = new Tree({
		"seed": 262,
		"segments": 6,
		"levels": 5,
		"vMultiplier": 2.36,
		"twigScale": 0.39,
		"initalBranchLength": 0.49,
		"lengthFalloffFactor": 0.85,
		"lengthFalloffPower": 0.99,
		"clumpMax": 0.454,
		"clumpMin": 0.404,
		"branchFactor": 2.45,
		"dropAmount": -0.1,
		"growAmount": 0.235,
		"sweepAmount": 0.01,
		"maxRadius": 0.139,
		"climbRate": 0.371,
		"trunkKink": 0.093,
		"treeSteps": 5,
		"taperRate": 0.947,
		"radiusFalloffRate": 0.73,
		"twistRate": 3.02,
		"trunkLength": 2.4
	});
	var treeMesh = new GLGE.Mesh({
		Positions: Tree.flattenArray(myTree.verts),
		Normals: Tree.flattenArray(myTree.normals),
		UV: Tree.flattenArray(myTree.UV),
		Faces: Tree.flattenArray(myTree.Faces),
	});

	var twigMesh = new GLGE.Mesh({
		Positions: Tree.flattenArray(myTree.vertsTwig),
		Normals: Tree.flattenArray(myTree.normalsTwig),
		UV: Tree.flattenArray(myTree.uvsTwig),
		Faces: Tree.flattenArray(myTree.facesTwig),
	});
</script>
```

#### Three.js

Mesh creation, [Three.js](https://github.com/mrdoob/three.js/) example:
```javascript
// Helper function to transform the vertices and faces
function newTreeGeometry(tree, isTwigs) {
  var output = new THREE.Geometry();

  tree[ isTwigs ? 'vertsTwig' : 'verts'].forEach(function(v) {
    output.vertices.push(new THREE.Vector3(v[0], v[1], v[2]));
  });

  var uv = isTwigs ? tree.uvsTwig : tree.UV;
  tree[ isTwigs ? 'facesTwig' : 'faces'].forEach(function(f) {
    output.faces.push(new THREE.Face3(f[0], f[1], f[2]));
    output.faceVertexUvs[0].push(f.map(function(v) {
      return new THREE.Vector2(uv[v][0], uv[v][1]);
    }));
  });

  output.computeFaceNormals();
  output.computeVertexNormals(true);

  return output;
}

var myTree = new Tree(/* same parameters as previous example */);

var trunkGeo = newTreeGeometry(tree);
var trunkMaterial = new THREE.MeshLambertMaterial( { color: 0xdddddd, wireframe: false } );
var trunkMesh = new THREE.Mesh(trunkGeo, trunkMaterial);
scene.add(trunkMesh); // Use your own scene

var twigsGeo = newTreeGeometry(tree, true);
var twigsMaterial = new THREE.MeshLambertMaterial( { color: 0x999999, wireframe: false } );
var twigsMesh = new THREE.Mesh(twigsGeo, twigsMaterial);
scene.add(twigsMesh); // Use your own scene

```

