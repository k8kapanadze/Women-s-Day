import React, { useState } from 'react';

const GiftIdea = () => {
  const [recipient, setRecipient] = useState('partner');
  const [budget, setBudget] = useState(100);

  const plans = [
    { id: 1, type: 'partner', min: 0, max: 150, title: "რომანტიკული კინო-ღამე", desc: "პრემიუმ ტკბილეული + 2 ბილეთი + კურიერი კოსტუმში" },
    { id: 2, type: 'partner', min: 151, max: 500, title: "ვახშამი ვარსკვლავების ქვეშ", desc: "ტერასის დაჯავშნა + პერსონალური მენიუ + ვიოლინო" },
    { id: 3, type: 'mother', min: 0, max: 1000, title: "სპა და რელაქსაცია", desc: "სრული დღის აბონემენტი + ტრანსპორტირება + ყვავილები" },
    { id: 4, type: 'colleague', min: 0, max: 100, title: "ოფისის სიურპრიზი", desc: "პერსონალიზებული ყუთი + პრემიუმ ყავის ნაკრები" },
  ];

  const filteredPlans = plans.filter(p => p.type === recipient && budget <= p.max);

  return (
    <div className="min-h-screen bg-slate-900 text-white p-8 font-sans">
      <div className="max-w-4xl mx-auto">
        <header className="text-center mb-12">
          <h1 className="text-4xl font-bold text-amber-400 mb-2">Surprise Planner</h1>
          <p className="text-slate-400">აქციე 8 მარტი დაუვიწყარ მოგონებად</p>
        </header>

        {/* სელექტორების სექცია */}
        <div className="grid grid-cols-1 md:grid-cols-2 gap-8 bg-slate-800 p-8 rounded-2xl shadow-2xl border border-slate-700 mb-8">
          <div>
            <label className="block mb-4 text-sm uppercase tracking-widest text-slate-400">ვისთვის?</label>
            <select 
              className="w-full bg-slate-700 p-3 rounded-lg outline-none focus:ring-2 focus:ring-amber-500"
              onChange={(e) => setRecipient(e.target.value)}
            >
              <option value="partner">მეუღლე / პარტნიორი</option>
              <option value="mother">დედა</option>
              <option value="colleague">კოლეგა</option>
            </select>
          </div>

          <div>
            <label className="block mb-4 text-sm uppercase tracking-widest text-slate-400">ბიუჯეტი: {budget} ₾</label>
            <input 
              type="range" min="50" max="1000" step="50" 
              className="w-full h-2 bg-slate-700 rounded-lg appearance-none cursor-pointer accent-amber-500"
              onChange={(e) => setBudget(e.target.value)}
            />
          </div>
        </div>

        {/* შედეგების სექცია */}
        <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
          {filteredPlans.map(plan => (
            <div key={plan.id} className="bg-slate-800 border-l-4 border-amber-500 p-6 rounded-xl hover:scale-105 transition-transform duration-300">
              <h3 className="text-xl font-bold mb-2">{plan.title}</h3>
              <p className="text-slate-400 mb-4">{plan.desc}</p>
              <button className="bg-amber-500 hover:bg-amber-600 text-slate-900 font-bold py-2 px-6 rounded-full transition-colors">
                დაჯავშნა
              </button>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

export default GiftIdea;
