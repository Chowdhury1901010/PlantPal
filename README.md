import React, { useState, useEffect } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button";

const PlantPalApp = () => { const [plants, setPlants] = useState([]); const [name, setName] = useState(""); const [type, setType] = useState("");

const addPlant = () => { if (name && type) { setPlants([...plants, { name, type, lastWatered: new Date() }]); setName(""); setType(""); } };

const waterPlant = (index) => { const updatedPlants = [...plants]; updatedPlants[index].lastWatered = new Date(); setPlants(updatedPlants); };

return ( <div className="p-4 max-w-2xl mx-auto"> <h1 className="text-3xl font-bold mb-4">PlantPal 🌱</h1>

<div className="mb-4 grid grid-cols-1 md:grid-cols-2 gap-2">
    <input
      type="text"
      placeholder="Plant Name"
      className="border rounded p-2"
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
    <input
      type="text"
      placeholder="Plant Type"
      className="border rounded p-2"
      value={type}
      onChange={(e) => setType(e.target.value)}
    />
    <Button onClick={addPlant} className="col-span-1 md:col-span-2">
      Add Plant
    </Button>
  </div>

  <div className="grid gap-4">
    {plants.map((plant, index) => (
      <Card key={index} className="shadow-md">
        <CardContent className="p-4">
          <h2 className="text-xl font-semibold">{plant.name}</h2>
          <p className="text-gray-600">Type: {plant.type}</p>
          <p className="text-sm text-gray-500">
            Last Watered: {new Date(plant.lastWatered).toLocaleString()}
          </p>
          <Button
            onClick={() => waterPlant(index)}
            className="mt-2"
          >
            Water Now
          </Button>
        </CardContent>
      </Card>
    ))}
  </div>
</div>

); };

export default PlantPalApp;

