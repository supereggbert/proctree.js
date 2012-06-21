proctree.js
===========

Procedural tree creation library
    
### Usage ###
	
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