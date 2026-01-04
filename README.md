import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";

export default function ZapacleanWeb() {
  const [selection, setSelection] = useState([]);

  const services = [
    { id: "basic", title: "Limpieza Esencial", desc: "Uso diario, mantenimiento fino" },
    { id: "deep", title: "Deep Clean", desc: "Suciedad profunda, telas y suelas" },
    { id: "premium", title: "Restauración Premium", desc: "Zapatillas de alto valor" },
  ];

  const toggle = (id) => {
    setSelection((prev) =>
      prev.includes(id) ? prev.filter((s) => s !== id) : [...prev, id]
    );
  };

  const whatsappLink = `https://wa.me/51999999999?text=${encodeURIComponent(
    `Hola, necesito el siguiente servicio: ${selection.join(", ")}`
  )}`;

  return (
    <div className="min-h-screen bg-black text-neutral-200 px-6 py-12 font-sans">
      <motion.h1
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        className="text-4xl md:text-5xl font-light tracking-wide mb-4"
      >
        Tilín Zapaclean
      </motion.h1>

      <p className="max-w-xl text-neutral-400 mb-12">
        Limpieza especializada de zapatillas. Tú decides qué necesitas. Nosotros lo ejecutamos.
      </p>

      <div className="grid md:grid-cols-3 gap-6 mb-12">
        {services.map((s) => (
          <Card
            key={s.id}
            onClick={() => toggle(s.id)}
            className={`cursor-pointer border transition-all bg-neutral-900 ${
              selection.includes(s.id)
                ? "border-yellow-500"
                : "border-neutral-800"
            }`}
          >
            <CardContent className="p-6">
              <h2 className="text-xl mb-2">{s.title}</h2>
              <p className="text-neutral-400 text-sm">{s.desc}</p>
            </CardContent>
          </Card>
        ))}
      </div>

      <div className="flex flex-col md:flex-row gap-4 items-start">
        <Button
          asChild
          disabled={selection.length === 0}
          className="bg-yellow-500 text-black hover:bg-yellow-400"
        >
          <a href={whatsappLink} target="_blank" rel="noreferrer">
            Continuar por WhatsApp
          </a>
        </Button>

        <p className="text-neutral-500 text-sm max-w-sm">
          No formularios. No llamadas incómodas. Solo eliges lo que quieres y nos escribes.
        </p>
      </div>
    </div>
  );
}
