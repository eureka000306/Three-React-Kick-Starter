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
<br/>
import { useFrame } from "@react-three/fiber";
<br/>
 
function Cylinder3d(props) {<br/>
  // This reference gives us direct access to the THREE.Mesh object<br/>
  const ref = useRef();<br/>
  // Hold state for hovered and clicked events<br/>
  const [hovered, hover] = useState(false);<br/>
  const [clicked, click] = useState(false);<br/>
  // Subscribe this component to the render-loop, rotate the mesh every frame<br/>
  useFrame((state, delta) => (ref.current.rotation.x += 0.01));<br/>
  // Return the view, these are regular Threejs elements expressed in JSX<br/>
  return (<br/>
    <mesh<br/>
      {...props}<br/>
      ref={ref}<br/>
      scale={clicked ? 1.5 : 1}<br/>
      onClick={(event) => click(!clicked)}<br/>
      onPointerOver={(event) => hover(true)}<br/>
      onPointerOut={(event) => hover(false)}<br/>
    ><br/>
      <cylinderGeometry args={[1, 1, 1]} /><br/>
      <meshStandardMaterial<br/>
        wireframe={props.wireframe}<br/>
        color={hovered ? "hotpink" : "orange"}<br/>
      /><br/>
    </mesh><br/>
  );<br/>
}<br/>
export default Cylinder3d;<br/>

# Replace App.js with this code lines
import "./App.css";<br/>
import { Canvas } from "@react-three/fiber";<br/>
import Cylinder3d from "./component/Cylinder3d";<br/>
 <br/>
function App() {<br/>
  return (<br/>
    <>
      <section className='App-header'>
        <Canvas>
          {/* <pointLight position={[10, 10, 10]} /> */}<br/>
          {/* <ambientLight /> */}<br/>
          <Cylinder3d position={[-1.2, 0, 0]} /><br/>
          <Cylinder3d position={[1.2, 0, 0]} /><br/>
        </Canvas>
      </section>
    </><br/>
  );<br/>
}<br/>
 <br/>
export default App;<br/>

# Uncomment code lines in App.js to see light effect

# Update App.js file with code below

import "./App.css";<br/>
import { Canvas } from "@react-three/fiber";<br/>
import Cylinder3d from "./component/Cylinder3d";<br/>
<br/>
function App() {<br/>
  return (<br/>
    <>
      <section className='App-header'>
        {/* Canvas 1 */}<br/>
        <Canvas><br/>
          <pointLight position={[10, 10, 10]} /><br/>
          <ambientLight /><br/>
          <Cylinder3d position={[-1.2, 0, 0]} /><br/>
          <Cylinder3d position={[1.2, 0, 0]} />
        </Canvas><br/>
<br/>
        {/* Canvas 2 */}<br/>
        <Canvas><br/>
          <pointLight position={[10, 10, 10]} /><br/>
          <ambientLight intensity={0.5} /><br/>
          <Cylinder3d position={[-1.2, 0, 0]} wireframe={true} /><br/>
          <Cylinder3d position={[1.2, 0, 0]} wireframe={true} /><br/>
        </Canvas>
<br/>
        {/* Canvas 3 */}<br/>
        <Canvas><br/>
          <pointLight position={[10, 10, 10]} /><br/>
          <ambientLight color={"red"} /><br/>
          <Cylinder3d position={[-1.2, 0, 0]} /><br/>
          <Cylinder3d position={[1.2, 0, 0]} /><br/>
        </Canvas>
      </section><br/>
    </><br/>
  );<br/>
}<br/>
<br/>
export default App;<br/>