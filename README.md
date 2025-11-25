# portfolio-margo

import { motion } from "framer-motion";
import { useState, useEffect, useRef } from "react";
import { Home, FileText, Briefcase, Mail, Video } from "lucide-react";

// Portfolio App-style responsive single-file React component
// Tailwind classes assumed to be available in the project.

export default function PortfolioAppStyle() {
  const [openApp, setOpenApp] = useState(null);
  const touchStartX = useRef(null);

  // Example user data (pré-rempli avec les éléments pertinents de Margo)
  const user = {
    name: "Margo",
    title: "Étudiante en BUT Carrières Juridiques — Assistante juridique (ADK Avocats)",
    location: "Lyon, France",
    email: "margo@example.com",
    linkedin: "https://www.linkedin.com/in/margo-sample",
    about:
      "Je crée du contenu accessible autour de l'alimentation sans culpabilité et j'intégrerai mes expériences juridiques (droit bancaire, assurances, dommage corporel).",
  };

  const apps = [
    {
      id: "cv",
      label: "CV",
      icon: FileText,
      content: (
        <div className="p-4 space-y-4">
          <div className="flex items-center gap-4">
            <div className="w-16 h-16 bg-gray-800 rounded-xl flex items-center justify-center text-2xl">MS</div>
            <div>
              <h3 className="text-lg font-semibold">{user.name}</h3>
              <p className="text-xs opacity-80">{user.title}</p>
              <p className="text-xs opacity-60">{user.location}</p>
            </div>
          </div>

          <section>
            <h4 className="text-sm font-medium">À propos</h4>
            <p className="text-xs opacity-80">{user.about}</p>
          </section>

          <section>
            <h4 className="text-sm font-medium">Expériences</h4>
            <ul className="text-xs opacity-80 list-disc list-inside">
              <li><strong>ADK Avocats</strong> — Assistante juridique (alternance) — Droit bancaire / assurances</li>
              <li><strong>Projets universitaires</strong> — Mémoire et rapport d'activité (BUT Carrières Juridiques)</li>
            </ul>
          </section>

          <section>
            <h4 className="text-sm font-medium">Compétences</h4>
            <div className="flex flex-wrap gap-2">
              {['Rédaction juridique','Recherche','Droit bancaire','Montages vidéo courts','Création de contenu'].map(s => (
                <span key={s} className="text-xs bg-gray-800 px-2 py-1 rounded">{s}</span>
              ))}
            </div>
          </section>

          <div className="flex gap-2 mt-2">
            <a href={user.linkedin} target="_blank" rel="noreferrer" className="text-xs underline">LinkedIn</a>
            <a href={`mailto:${user.email}`} className="text-xs underline">Email</a>
          </div>
        </div>
      ),
    },
    {
      id: "projets",
      label: "Projets",
      icon: Briefcase,
      content: (
        <div className="p-4 space-y-4">
          <h3 className="text-lg font-semibold">Projets sélectionnés</h3>

          <div className="grid gap-3">
            <article className="p-3 bg-gray-900 rounded-lg shadow-sm">
              <h4 className="font-medium">Mémoire de droit — Secteur des activités juridiques (APE 6910Z)</h4>
              <p className="text-xs opacity-80">Analyse du secteur sur 5 pages : structure, enjeux et perspectives — inclut droit bancaire.</p>
            </article>

            <article className="p-3 bg-gray-900 rounded-lg shadow-sm">
              <h4 className="font-medium">Rapport d'activité — Alternance chez ADK Avocats</h4>
              <p className="text-xs opacity-80">Présentation du cabinet, missions effectuées, retours d'expérience en droit bancaire et assurances.</p>
            </article>

            <article className="p-3 bg-gray-900 rounded-lg shadow-sm">
              <h4 className="font-medium">Projet audiovisuel — "La Voie de la justice" (Just Mercy)</h4>
              <p className="text-xs opacity-80">Analyse et projet de médiation autour du film pour illustrer l'importance de l'accès à la justice.</p>
            </article>
          </div>

          <div className="mt-2 flex gap-2">
            <button className="text-xs px-3 py-2 bg-white bg-opacity-5 rounded">Télécharger dossier (PDF)</button>
            <button className="text-xs px-3 py-2 bg-white bg-opacity-5 rounded">Voir tous les projets</button>
          </div>
        </div>
      ),
    },
    
    {
      id: "videos",
      label: "Vidéos",
      icon: Video,
      content: (
        <div className="p-4 space-y-4">
          <h3 className="text-lg font-semibold">Vidéos courtes</h3>
          <p className="text-xs opacity-70">Exemples de formats courts (TikTok / montage "Bref").</p>
          <div className="grid grid-cols-1 gap-3">
            <div className="h-36 bg-gray-900 rounded-lg flex items-center justify-center">Vidéo TikTok 1</div>
            <div className="h-36 bg-gray-900 rounded-lg flex items-center justify-center">Vidéo TikTok 2</div>
          </div>
        </div>
      ),
    },
    { id: "contact",
      label: "Contact",
      icon: Mail,
      content: (
        <div className="p-4 space-y-4">
          <h3 className="text-lg font-semibold">Contact</h3>
          <p className="text-xs opacity-80">Tu peux proposer un formulaire ou des liens directs.</p>

          <form className="space-y-2" onSubmit={(e) => { e.preventDefault(); alert('Merci — formulaire simulé (à relier au backend).'); }}>
            <input placeholder="Ton nom" className="w-full p-2 bg-gray-800 rounded text-xs" />
            <input placeholder="Ton email" className="w-full p-2 bg-gray-800 rounded text-xs" />
            <textarea placeholder="Message" className="w-full p-2 bg-gray-800 rounded text-xs h-24" />
            <div className="flex gap-2">
              <button type="submit" className="px-3 py-2 text-xs bg-white bg-opacity-5 rounded">Envoyer</button>
              <a href={`mailto:${user.email}`} className="px-3 py-2 text-xs bg-white bg-opacity-5 rounded">Email direct</a>
            </div>
          </form>

          <div className="text-xs opacity-70">Links: <a href={user.linkedin} target="_blank" rel="noreferrer" className="underline">LinkedIn</a></div>
        </div>
      ),
    },
  ];

  useEffect(() => {
    // prevent body scroll when app is open on small screens
    document.body.style.overflow = openApp ? 'hidden' : '';
    return () => { document.body.style.overflow = ''; };
  }, [openApp]);

  // Simple touch handlers to swipe back
  function onTouchStart(e) {
    touchStartX.current = e.touches[0].clientX;
  }
  function onTouchEnd(e) {
    if (!touchStartX.current) return;
    const delta = e.changedTouches[0].clientX - touchStartX.current;
    if (delta > 60) setOpenApp(null); // swipe right to close
    touchStartX.current = null;
  }

  return (
    <div className="w-full min-h-screen bg-gradient-to-br from-gray-900 to-black flex flex-col items-center justify-between py-12 text-white">
      {/* Faux téléphone */}
      <div className="w-[360px] sm:w-[390px] h-[740px] bg-black rounded-[44px] border-4 border-gray-700 shadow-2xl flex flex-col items-center p-4 relative overflow-hidden">
        {/* Notch */}
        <div className="w-44 h-6 bg-gray-800 rounded-b-3xl absolute top-0"></div>

        {/* Home / Apps */}
        {!openApp && (
          <motion.div
            className="grid grid-cols-3 gap-5 mt-16"
            initial={{ opacity: 0, y: 10 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ staggerChildren: 0.05 }}
          >
            {apps.map((app) => (
              <motion.button
                key={app.id}
                onClick={() => setOpenApp(app.id)}
                whileTap={{ scale: 0.96 }}
                className="flex flex-col items-center"
              >
                <div className="w-20 h-20 bg-gray-800 rounded-2xl flex items-center justify-center shadow-lg">
                  <app.icon size={28} />
                </div>
                <p className="text-xs mt-2 opacity-80">{app.label}</p>
              </motion.button>
            ))}
          </motion.div>
        )}

        {/* Open app view */}
        {openApp && (
          <motion.div
            onTouchStart={onTouchStart}
            onTouchEnd={onTouchEnd}
            initial={{ opacity: 0, x: 50 }}
            animate={{ opacity: 1, x: 0 }}
            exit={{ opacity: 0, x: 50 }}
            transition={{ type: 'spring', stiffness: 300, damping: 30 }}
            className="absolute inset-0 bg-black overflow-auto"
          >
            <div className="w-full flex items-center justify-between p-3 bg-gray-900 bg-opacity-80 sticky top-0">
              <button onClick={() => setOpenApp(null)} className="text-xl">←</button>
              <h2 className="text-sm font-medium capitalize">{openApp}</h2>
              <div className="text-xs opacity-60">{user.name}</div>
            </div>

            {apps.find(a => a.id === openApp)?.content}
          </motion.div>
        )}
      </div>

      {/* Dock */}
      <div className="w-[340px] sm:w-[380px] h-20 bg-white bg-opacity-8 rounded-3xl backdrop-blur-xl flex items-center justify-around p-3 mt-6">
        <button onClick={() => setOpenApp(null)} className="p-2"><Home /></button>
        <button onClick={() => setOpenApp('cv')} className="p-2"><FileText /></button>
        <button onClick={() => setOpenApp('projets')} className="p-2"><Briefcase /></button>
        <button onClick={() => setOpenApp('contact')} className="p-2"><Mail /></button>
      </div>
    </div>
  );
}
