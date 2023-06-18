# Getting Started with Create React App

npx create-react-app my-3d-react-app
<br/>
cd my-3d-react-app

# Install Three.js modules

npm install three @react-three/fiber
mkdir src\component

# Create Cylinder3d file

type nul > Cylinder3d.jsx
<br/>
type nul > src\component\Cylinder3d.jsx

# Fill the Cylinder3d.jsx file with following code lines
import React, { useRef, useState } from "react";
import { useFrame } from "@react-three/fiber";
 
function Cylinder3d(props) {
  // This reference gives us direct access to the THREE.Mesh object
  const ref = useRef();
  // Hold state for hovered and clicked events
  const [hovered, hover] = useState(false);
  const [clicked, click] = useState(false);
  // Subscribe this component to the render-loop, rotate the mesh every frame
  useFrame((state, delta) => (ref.current.rotation.x += 0.01));
  // Return the view, these are regular Threejs elements expressed in JSX
  return (
    <mesh
      {...props}
      ref={ref}
      scale={clicked ? 1.5 : 1}
      onClick={(event) => click(!clicked)}
      onPointerOver={(event) => hover(true)}
      onPointerOut={(event) => hover(false)}
    >
      <cylinderGeometry args={[1, 1, 1]} />
      <meshStandardMaterial
        wireframe={props.wireframe}
        color={hovered ? "hotpink" : "orange"}
      />
    </mesh>
  );
}
 
export default Cylinder3d;


# Replace App.js with this code lines
import "./App.css";
import { Canvas } from "@react-three/fiber";
import Cylinder3d from "./component/Cylinder3d";
 
function App() {
  return (
    <>
      <section className='App-header'>
        <Canvas>
          {/* <pointLight position={[10, 10, 10]} /> */}
          {/* <ambientLight /> */}
          <Cylinder3d position={[-1.2, 0, 0]} />
          <Cylinder3d position={[1.2, 0, 0]} />
        </Canvas>
      </section>
    </>
  );
}
 
export default App;

# Uncomment code lines in App.js to see light effect

# Update App.js file

import "./App.css";
import { Canvas } from "@react-three/fiber";
import Cylinder3d from "./component/Cylinder3d";

function App() {
  return (
    <>
      <section className='App-header'>
        {/* Canvas 1 */}
        <Canvas>
          <pointLight position={[10, 10, 10]} />
          <ambientLight />
          <Cylinder3d position={[-1.2, 0, 0]} />
          <Cylinder3d position={[1.2, 0, 0]} />
        </Canvas>

        {/* Canvas 2 */}
        <Canvas>
          <pointLight position={[10, 10, 10]} />
          <ambientLight intensity={0.5} />
          <Cylinder3d position={[-1.2, 0, 0]} wireframe={true} />
          <Cylinder3d position={[1.2, 0, 0]} wireframe={true} />
        </Canvas>

        {/* Canvas 3 */}
        <Canvas>
          <pointLight position={[10, 10, 10]} />
          <ambientLight color={"red"} />
          <Cylinder3d position={[-1.2, 0, 0]} />
          <Cylinder3d position={[1.2, 0, 0]} />
        </Canvas>
      </section>
    </>
  );
}

See Full Tutorial <a href="https://www.copycat.dev/blog/react-three-fiber/" target="_blank">Here</a>