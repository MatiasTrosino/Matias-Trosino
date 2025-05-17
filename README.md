import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";
import { useState } from "react";

export default function HomePage() {
  const [troboInput, setTroboInput] = useState("");
  const [troboResponse, setTroboResponse] = useState("");

  const handleTroboChat = async () => {
    if (troboInput.trim() === "") return;
    setTroboResponse("Pensando...");
    try {
      const response = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${process.env.NEXT_PUBLIC_OPENAI_API_KEY}`,
        },
        body: JSON.stringify({
          model: "gpt-4",
          messages: [{ role: "user", content: troboInput }],
        }),
      });
      const data = await response.json();
      if (data.choices && data.choices.length > 0) {
        setTroboResponse(data.choices[0].message.content);
      } else {
        setTroboResponse("No se recibió una respuesta válida. Inténtalo de nuevo.");
      }
    } catch (error) {
      setTroboResponse("Lo siento, algo salió mal. Inténtalo de nuevo más tarde.");
    }
    setTroboInput("");
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-blue-900 to-black text-white px-6 py-10">
      <div className="text-center space-y-6">
        <h1 className="text-5xl font-bold tracking-tight">Matías Trosino</h1>
        <p className="text-lg">Escritura y Traducción | Servicios de IA | Crecimiento Personal</p>
        <p className="mt-4 text-base max-w-2xl mx-auto">¡Hola! Soy Matías Trosino. Me apasiona escribir, traducir y ayudar a otros a crecer tanto en lo personal como en lo digital. Con más de 5 años creando contenido, sé lo importante que es conectar con tu audiencia y transmitir ideas claras y poderosas. Ofrezco servicios de redacción y traducción en inglés y español, creación de prompts para IA y asesoría en crecimiento personal. Si buscas a alguien que cuide cada palabra y entienda el valor de un buen mensaje, hablemos. Estoy aquí para que tus ideas brillen.</p>
        <a href="https://wa.me/522225041889" target="_blank">
          <Button className="bg-teal-500 hover:bg-teal-600 text-white py-3 px-6 rounded-2xl shadow-lg transition-all mt-4">
            Escríbeme por WhatsApp
          </Button>
        </a>
      </div>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-8 mt-16">
        <a href="#escritura-traduccion" className="no-underline">
          <Card className="bg-gray-900 text-white rounded-2xl shadow-xl hover:scale-105 transition-transform">
            <CardContent>
              <h2 className="text-2xl font-semibold">Escritura y Traducción</h2>
              <p className="mt-2">Redacción profesional, traducción precisa y textos que conectan.</p>
            </CardContent>
          </Card>
        </a>
        <a href="#servicios-ia" className="no-underline">
          <Card className="bg-gray-900 text-white rounded-2xl shadow-xl hover:scale-105 transition-transform">
            <CardContent>
              <h2 className="text-2xl font-semibold">Servicios de IA</h2>
              <p className="mt-2">Prompts personalizados y soluciones inteligentes para tus proyectos.</p>
            </CardContent>
          </Card>
        </a>
        <a href="#crecimiento-personal" className="no-underline">
          <Card className="bg-gray-900 text-white rounded-2xl shadow-xl hover:scale-105 transition-transform">
            <CardContent>
              <h2 className="text-2xl font-semibold">Crecimiento Personal</h2>
              <p className="mt-2">Asesoría y estrategias para alcanzar tus metas personales.</p>
            </CardContent>
          </Card>
        </a>
      </div>
      <div id="escritura-traduccion" className="mt-24 space-y-4">
        <h2 className="text-4xl font-bold text-center">Escritura y Traducción</h2>
        <p className="text-center text-lg max-w-3xl mx-auto">Redacción profesional, traducción precisa y textos que conectan. Desde artículos impactantes hasta traducciones exactas que mantienen el sentido y la intención original del mensaje.</p>
      </div>
      <div id="servicios-ia" className="mt-24 space-y-4">
        <h2 className="text-4xl font-bold text-center">Servicios de IA</h2>
        <p className="text-center text-lg max-w-3xl mx-auto">Prompts personalizados y soluciones inteligentes para optimizar tus proyectos. Saca el máximo provecho de la inteligencia artificial para hacer crecer tu negocio.</p>
      </div>
      <div id="crecimiento-personal" className="mt-24 space-y-4">
        <h2 className="text-4xl font-bold text-center">Crecimiento Personal</h2>
        <p className="text-center text-lg max-w-3xl mx-auto">Asesoría personalizada para alcanzar tus metas y mejorar cada día. Transforma tus hábitos, desbloquea tu potencial y logra el éxito que mereces.</p>
      </div>
    </div>
  );
}
# Matias-Trosino
Este sitio web es para fiverr
