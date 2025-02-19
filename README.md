import { useState } from "react";
import { Menu, X } from "lucide-react";
import { Dialog } from "@headlessui/react";

const categories = {
  Tours: ["Location", "Duration", "Price"],
  Tickets: ["Event Type", "Date", "Price"],
  Rent: ["Vehicle Type", "Rental Period", "Price"],
  Transfer: ["Pickup Location", "Dropoff Location", "Price"],
};

export default function Navbar() {
  const [isOpen, setIsOpen] = useState(false);
  const [selectedCategory, setSelectedCategory] = useState(null);

  return (
    <nav className="bg-primary-500 p-4 flex justify-between items-center">
      <h1 className="text-white text-xl font-bold">Site Logo</h1>
      <button className="text-white" onClick={() => setIsOpen(true)}>
        <Menu size={28} />
      </button>
      
      <Dialog open={isOpen} onClose={() => setIsOpen(false)} className="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
        <div className="bg-white rounded-lg p-6 w-80">
          <div className="flex justify-between items-center mb-4">
            <h2 className="text-lg font-semibold">Select Category</h2>
            <button onClick={() => setIsOpen(false)}>
              <X size={24} />
            </button>
          </div>
          <ul className="space-y-2">
            {Object.keys(categories).map((category) => (
              <li key={category}>
                <button
                  className={`w-full text-left px-4 py-2 rounded-lg ${selectedCategory === category ? "bg-primary-400 text-white" : "bg-gray-200"}`}
                  onClick={() => setSelectedCategory(category)}
                >
                  {category}
                </button>
              </li>
            ))}
          </ul>
          {selectedCategory && (
            <div className="mt-4">
              <h3 className="text-md font-semibold">Filters for {selectedCategory}</h3>
              <ul className="mt-2 space-y-2">
                {categories[selectedCategory].map((filter) => (
                  <li key={filter} className="bg-gray-100 px-4 py-2 rounded-lg">{filter}</li>
                ))}
              </ul>
            </div>
          )}
        </div>
      </Dialog>
    </nav>
  );
}
