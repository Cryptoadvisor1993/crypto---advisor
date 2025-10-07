# crypto---advisor
Web profesional de asesoramiento sobre criptomonedas (Blockchain, Wallets, Trading, DApps, Staking, etc.)
/my-crypto-advice
├─ /app or /pages
│  ├─ index.jsx
│  ├─ /services
│  │   └─ [slug].jsx
│  ├─ /blog
│  ├─ /dashboard
├─ /components
│  ├─ Header.jsx
│  ├─ Footer.jsx
│  ├─ ServiceCard.jsx
│  └─ PriceTicker.jsx
├─ /lib
│  ├─ coingecko.js
│  ├─ openai.js
├─ /styles
├─ tailwind.config.js
├─ package.json
// components/ServiceCard.jsx
export default function ServiceCard({title, subtitle, icon}) {Blockguide,  Asesoría cripto clara para gente joven, paleta: (fondo: #0b1020 (negro azul) , acento 1: #00f5a0 (verde neón suave) , acento 2: #7c3aed (violeta) , textos: blancos y grises (#e6eef8, #9aa4b2) , tipografía:Inter (principal) , JetBrains Mono para code snippets , iconografía: lucide/react o heroicons — simple y lineal , estética: minimal, cards con blur y sutiles gradientes, microinteracciones (hover, scale))}
return (
    <div className="bg-gradient-to-br from-white/3 to-white/2 backdrop-blur-md border border-white/6 rounded-2xl p-6 shadow-lg hover:scale-101 transition-transform">
      <div className="w-14 h-14 rounded-xl flex items-center justify-center mb-4 bg-white/6">
        {icon}
      </div>
      <h3 className="text-xl font-semibold">{title}</h3>
      <p className="mt-2 text-sm text-slate-300">{subtitle}</p>
      <button className="mt-4 inline-block text-sm px-4 py-2 rounded-lg bg-emerald-500 hover:bg-emerald-600 text-black font-medium">
        Saber más
      </button>
    </div>
    
// pages/index.jsx  (o app/page.jsx)
import ServiceCard from '../components/ServiceCard'
import { FaDiceD6, FaWallet, FaExchangeAlt, FaFileInvoiceDollar } from 'react-icons/fa'

export default function Home() {
  return (
    <main className="min-h-screen bg-gradient-to-b from-slate-900 via-black to-slate-900 text-white">
      <header className="max-w-6xl mx-auto py-6 px-4 flex justify-between items-center">
        <div className="flex items-center gap-3">
          <div className="w-10 h-10 bg-gradient-to-br from-emerald-400 to-violet-500 rounded-xl flex items-center justify-center font-bold">CW</div>
          <span className="font-semibold">CryptoAdvisors</span>
        </div>
        <nav className="flex gap-6">
          <a>Inicio</a><a>Servicios</a><a>Blog</a><a>Contacto</a>
        </nav>
      </header>

      <section className="text-center pt-16 pb-12 px-4">
        <h1 className="text-4xl md:text-5xl font-bold max-w-3xl mx-auto">Asesoramiento cripto profesional — explicado fácil</h1>
        <p className="mt-4 text-slate-300 max-w-2xl mx-auto">Te ayudamos con wallets, exchanges, impuestos, staking, nodos y estrategias de trading sin complicarlo. Para jóvenes que quieren hacerlo bien desde el principio.</p>
        <div className="mt-8 flex justify-center gap-4">
          <button className="bg-emerald-500 hover:bg-emerald-600 px-6 py-3 rounded-xl font-semibold text-black">Empieza tu asesoramiento cripto</button>
          <button className="border border-white/20 px-5 py-3 rounded-xl">Ver servicios</button>
        </div>
      </section>

      <section className="max-w-6xl mx-auto px-4 py-12">
        <h2 className="text-2xl font-semibold mb-6">Servicios</h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
          <ServiceCard title="Blockchain" subtitle="Arquitectura, L1/L2 y casos de uso" icon={<FaDiceD6 />} />
          <ServiceCard title="Wallets" subtitle="Setup seguro, hardware y best practices" icon={<FaWallet />} />
          <ServiceCard title="Exchanges" subtitle="Cómo usar, comparar y transferir" icon={<FaExchangeAlt />} />
          <ServiceCard title="Impuestos" subtitle="Declaración y optimización fiscal" icon={<FaFileInvoiceDollar />} />
          {/* añade más tarjetas según necesites */}
        </div>
      </section>

      <footer className="py-8 text-center text-sm text-slate-400">© {new Date().getFullYear()} CryptoAdvisors — No custodial, información educativa.</footer>
    </main>
  )
}
// pages/api/price.js
import fetch from 'node-fetch'

export default async function handler(req, res) {
  const { id = 'bitcoin' } = req.query
  const cg = `https://api.coingecko.com/api/v3/simple/price?ids=${id}&vs_currencies=usd`
  try {
    const r = await fetch(cg)
    const json = await r.json()
    res.status(200).json(json)
  } catch (e) {
    res.status(500).json({ error: 'failed to fetch' })
  }
}
