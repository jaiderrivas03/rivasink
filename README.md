import React, { useEffect, useState } from 'react';
import { motion } from 'framer-motion';

export default function MarketingAgencyR() {
  const fadeUp = {
    hidden: { opacity: 0, y: 40 },
    visible: { opacity: 1, y: 0 },
  };

  const services = [
    {
      title: 'Marketing Digital',
      text: 'Estrategias enfocadas en crecimiento, tráfico y conversiones en canales digitales.',
    },
    {
      title: 'Gestión de Redes Sociales',
      text: 'Creamos contenido premium y administramos tu presencia digital con enfoque de marca.',
    },
    {
      title: 'Branding',
      text: 'Construimos identidades visuales memorables que elevan el valor percibido de tu empresa.',
    },
  ];

  const stats = [
    { number: '150+', label: 'Campañas lanzadas' },
    { number: '98%', label: 'Clientes satisfechos' },
    { number: '24/7', label: 'Soporte creativo' },
  ];

  const [leads, setLeads] = useState([]);
  const [form, setForm] = useState({ name: '', email: '', message: '' });
  const [showCRM, setShowCRM] = useState(false);

  useEffect(() => {
    const stored = localStorage.getItem('rivasink_leads');
    if (stored) setLeads(JSON.parse(stored));
  }, []);

  const handleChange = (e) => {
    setForm({ ...form, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();

    const newLead = {
      ...form,
      id: Date.now(),
      date: new Date().toLocaleString(),
    };

    const updated = [newLead, ...leads];
    setLeads(updated);
    localStorage.setItem('rivasink_leads', JSON.stringify(updated));

    setForm({ name: '', email: '', message: '' });
    alert('Gracias por contactarnos. Te responderemos pronto.');
  };

  return (
    <div className="min-h-screen bg-[#f5f5f7] text-slate-900 overflow-x-hidden antialiased">
      <motion.header
        initial={{ y: -50, opacity: 0 }}
        animate={{ y: 0, opacity: 1 }}
        transition={{ duration: 0.8 }}
        className="bg-white/70 backdrop-blur-2xl border-b border-black/5 text-slate-900 sticky top-0 z-50"
      >
        <div className="max-w-7xl mx-auto px-6 py-6 flex items-center justify-between">
          <motion.h1
            whileHover={{ scale: 1.08 }}
            className="text-4xl font-semibold tracking-[0.35em] cursor-pointer text-slate-950"
          >Rivas Ink</motion.h1>

          <nav className="hidden md:flex gap-8 text-sm uppercase tracking-wide">
            <a href="#services" className="hover:text-blue-300 transition">Servicios</a>
            <a href="#about" className="hover:text-blue-300 transition">Nosotros</a>
            <a href="#contact" className="hover:text-blue-300 transition">Contacto</a>
            <button
              onClick={() => setShowCRM(!showCRM)}
              className="text-xs px-3 py-1 rounded-full bg-slate-900 text-white"
            >
              CRM
            </button>
          </nav>
        </div>
      </motion.header>

      <section className="bg-[#f5f5f7] text-slate-900 py-36 px-6 text-center relative overflow-hidden">
        <motion.div
          animate={{ scale: [1, 1.05, 1] }}
          transition={{ duration: 8, repeat: Infinity }}
          className="absolute w-[500px] h-[500px] bg-blue-500/10 rounded-full blur-3xl top-[-150px] right-[-120px]"
        />

        <motion.div
          variants={fadeUp}
          initial="hidden"
          animate="visible"
          className="max-w-5xl mx-auto relative z-10"
        >
          <div className="inline-flex items-center px-4 py-2 rounded-full bg-white border border-slate-200 shadow-sm mb-8 text-sm text-slate-700">
            Premium Marketing • Luxury Brand Experience
          </div>

          <h2 className="text-6xl md:text-8xl font-semibold mb-6 leading-[0.95] tracking-[-0.03em] text-slate-950">
            La nueva era del marketing premium
          </h2>

          <p className="text-xl text-slate-600 mb-12 max-w-3xl mx-auto font-light leading-relaxed">
            En Rivas Ink ayudamos a empresas a crecer con estrategias de marketing digital,
            branding y contenido que generan resultados reales.
          </p>

          <a
            href="#contact"
            className="inline-flex items-center bg-slate-950 px-8 py-4 rounded-full text-white"
          >
            Contáctanos
          </a>

          <div className="grid grid-cols-1 md:grid-cols-3 gap-6 mt-20">
            {stats.map((stat, i) => (
              <div key={i} className="bg-white/80 rounded-[2rem] p-8 border border-white">
                <div className="text-4xl font-semibold">{stat.number}</div>
                <div className="text-slate-500">{stat.label}</div>
              </div>
            ))}
          </div>
        </motion.div>
      </section>

      <section className="py-36 px-6 bg-white">
        <div className="max-w-6xl mx-auto text-center">
          <h3 className="text-5xl font-semibold mb-4">Experiencias que venden</h3>
          <p className="text-slate-500 text-lg mb-16">
            Creamos marcas memorables con diseño, estrategia y presencia premium.
          </p>
        </div>
      </section>

      <section id="services" className="py-36 px-6 bg-[#f5f5f7]">
        <div className="max-w-6xl mx-auto text-center">
          <h3 className="text-4xl font-bold mb-4">Servicios de Marketing</h3>
          <p className="text-slate-600 mb-12">Soluciones diseñadas para resultados.</p>

          <div className="grid md:grid-cols-3 gap-8">
            {services.map((s, i) => (
              <div key={i} className="bg-white p-10 rounded-[2.5rem] border border-white">
                <h4 className="text-2xl font-semibold mb-4">{s.title}</h4>
                <p className="text-slate-600">{s.text}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      <section id="contact" className="py-36 px-6 bg-[#0a0a0a] text-white">
        <div className="max-w-4xl mx-auto text-center">
          <h3 className="text-4xl font-bold mb-6">Contáctanos</h3>

          <form onSubmit={handleSubmit} className="space-y-4">
            <input
              name="name"
              value={form.name}
              onChange={handleChange}
              placeholder="Nombre"
              className="w-full p-4 rounded-xl text-black"
            />
            <input
              name="email"
              value={form.email}
              onChange={handleChange}
              placeholder="Email"
              className="w-full p-4 rounded-xl text-black"
            />
            <textarea
              name="message"
              value={form.message}
              onChange={handleChange}
              placeholder="Mensaje"
              className="w-full p-4 rounded-xl text-black"
            />
            <button className="bg-white text-black px-8 py-4 rounded-full">
              Enviar
            </button>
          </form>
        </div>
      </section>

      {showCRM && (
        <section className="p-10 bg-white">
          <h3 className="text-3xl font-bold mb-6">CRM - Leads</h3>
          <div className="space-y-4">
            {leads.map((l) => (
              <div key={l.id} className="p-4 border rounded-xl">
                <p><b>{l.name}</b> ({l.email})</p>
                <p className="text-sm text-slate-500">{l.message}</p>
                <p className="text-xs text-slate-400">{l.date}</p>
              </div>
            ))}
          </div>
        </section>
      )}

      <footer className="bg-black text-slate-400 py-6 text-center text-sm">
        © 2026 Rivas Ink — Premium Marketing Agency
      </footer>
    </div>
  );
}
