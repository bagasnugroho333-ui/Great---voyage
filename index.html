import { useState, useCallback, useRef } from "react";
import * as XLSX from "xlsx";
import {
  AreaChart, Area, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer
} from "recharts";
import { Anchor, AlertTriangle, Download, Upload, Wind, Compass } from "lucide-react";

// ─── CONSTANTS ────────────────────────────────────────────────────────────────
const NAVY = "#0A192F";
const NAVY2 = "#0D2137";
const GOLD = "#C5A059";
const GOLD_LIGHT = "#E8C97A";
const TEAL = "#2DD4BF";
const RED = "#EF4444";
const GREEN = "#22C55E";

const REQUIRED_FUEL_COLS = ["Bulan_On", "Bulan_Off", "Gaji_Laut", "Biaya_Laut", "Biaya_Darat"];
const REQUIRED_PARTS_COLS = ["Nama_Aset", "Alokasi_Persen", "Return_Persen"];
const REQUIRED_TARGET_COLS = ["Target_Passive_Income"];

// ─── TEMPLATE GENERATOR ──────────────────────────────────────────────────────
function downloadTemplate() {
  const wb = XLSX.utils.book_new();

  const fuelData = [
    { Bulan_On: 8, Bulan_Off: 4, Gaji_Laut: 3000, Biaya_Laut: 500, Biaya_Darat: 800 }
  ];
  const partsData = [
    { Nama_Aset: "Saham Dividen", Alokasi_Persen: 40, Return_Persen: 8 },
    { Nama_Aset: "Obligasi/Sukuk", Alokasi_Persen: 30, Return_Persen: 6 },
    { Nama_Aset: "REITs", Alokasi_Persen: 20, Return_Persen: 7 },
    { Nama_Aset: "Deposito", Alokasi_Persen: 10, Return_Persen: 5 }
  ];
  const targetData = [{ Target_Passive_Income: 2000 }];

  XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(fuelData), "Fueling");
  XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(partsData), "VesselParts");
  XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(targetData), "Target");

  XLSX.writeFile(wb, "GreatVoyage_Logbook_Template.xlsx");
}

// ─── CALCULATION ENGINE ──────────────────────────────────────────────────────
function calculate(fuelRow, parts, targetRow) {
  const { Bulan_On: on, Bulan_Off: off, Gaji_Laut: gaji, Biaya_Laut: biayaLaut, Biaya_Darat: biayaDarat } = fuelRow;
  const { Target_Passive_Income: targetPI } = targetRow;

  const annualFuel = (gaji * on) - (biayaLaut * on) - (biayaDarat * off);
  const totalMonths = on + off;
  const contractsPerYear = 12 / totalMonths;
  const annualSaving = annualFuel;

  // Weighted average return
  const weightedReturn = parts.reduce((acc, p) => {
    return acc + (p.Alokasi_Persen / 100) * (p.Return_Persen / 100);
  }, 0);

  // FIRE target: Target * 25 (4% rule)
  const fireCapital = targetPI * 12 * 25;

  // Projection: compound growth on accumulated portfolio
  const projectionData = [];
  let portfolio = 0;
  let salaryAccum = 0;
  const years = 30;

  for (let y = 1; y <= years; y++) {
    portfolio = (portfolio + annualSaving) * (1 + weightedReturn);
    salaryAccum += annualSaving;
    projectionData.push({
      year: `Thn ${y}`,
      Investasi: Math.round(portfolio),
      GajiSaja: Math.round(salaryAccum),
      FIRE: Math.round(fireCapital)
    });
  }

  // Voyage duration: how many contracts to reach FIRE
  let accum = 0;
  let contractCount = 0;
  while (accum < fireCapital && contractCount < 500) {
    accum = (accum + annualSaving / contractsPerYear) * (1 + weightedReturn / contractsPerYear);
    contractCount++;
  }

  const yearsToFIRE = contractCount / contractsPerYear;

  return { annualFuel, annualSaving, weightedReturn, fireCapital, projectionData, contractCount, yearsToFIRE, parts, targetPI, on, off, gaji };
}

// ─── VESSEL SVG ───────────────────────────────────────────────────────────────
function VesselSVG({ parts }) {
  const getColor = (idx) => {
    const colors = [GOLD, TEAL, "#A78BFA", "#F472B6", GREEN];
    return colors[idx % colors.length];
  };

  const engineAlloc = parts[0]?.Alokasi_Persen || 0;
  const hullAlloc = parts[1]?.Alokasi_Persen || 0;
  const lifeAlloc = parts[2]?.Alokasi_Persen || 0;
  const engineColor = parts[0] ? getColor(0) : "#334155";
  const hullColor = parts[1] ? getColor(1) : "#334155";
  const lifeColor = parts[2] ? getColor(2) : "#334155";

  return (
    <svg viewBox="0 0 280 180" xmlns="http://www.w3.org/2000/svg" style={{ width: "100%", maxWidth: 340, filter: "drop-shadow(0 0 24px rgba(197,160,89,0.18))" }}>
      <defs>
        <radialGradient id="engineGlow" cx="50%" cy="50%" r="50%">
          <stop offset="0%" stopColor={engineColor} stopOpacity="0.7" />
          <stop offset="100%" stopColor={engineColor} stopOpacity="0" />
        </radialGradient>
        <radialGradient id="hullGlow" cx="50%" cy="50%" r="50%">
          <stop offset="0%" stopColor={hullColor} stopOpacity="0.5" />
          <stop offset="100%" stopColor={hullColor} stopOpacity="0" />
        </radialGradient>
        <filter id="glow">
          <feGaussianBlur stdDeviation="2.5" result="coloredBlur" />
          <feMerge>
            <feMergeNode in="coloredBlur" />
            <feMergeNode in="SourceGraphic" />
          </feMerge>
        </filter>
      </defs>

      {/* Water */}
      <ellipse cx="140" cy="158" rx="120" ry="14" fill="#0D2137" opacity="0.8" />
      <path d="M20 155 Q60 148 100 155 Q140 162 180 155 Q220 148 260 155" stroke={TEAL} strokeWidth="1.5" fill="none" opacity="0.4" />

      {/* Hull */}
      <path d="M50 120 L60 145 L220 145 L230 120 Z" fill={hullColor} opacity="0.85" filter="url(#glow)" />
      <ellipse cx="140" cy="120" rx="80" ry="6" fill={hullColor} opacity="0.4" />
      <rect x="50" y="112" width="180" height="10" rx="2" fill={hullColor} opacity="0.6" />

      {/* Hull glow overlay */}
      <ellipse cx="140" cy="135" rx="90" ry="18" fill="url(#hullGlow)" />

      {/* Cabin / Superstructure */}
      <rect x="90" y="85" width="100" height="35" rx="4" fill="#0F2744" stroke={GOLD} strokeWidth="1.2" />
      <rect x="100" y="92" width="20" height="14" rx="2" fill={NAVY} stroke={TEAL} strokeWidth="0.8" opacity="0.9" />
      <rect x="128" y="92" width="20" height="14" rx="2" fill={NAVY} stroke={TEAL} strokeWidth="0.8" opacity="0.9" />
      <rect x="156" y="92" width="20" height="14" rx="2" fill={NAVY} stroke={TEAL} strokeWidth="0.8" opacity="0.9" />

      {/* Funnel / Engine stack */}
      <rect x="155" y="60" width="22" height="32" rx="3" fill={engineColor} opacity="0.9" filter="url(#glow)" />
      <rect x="160" y="52" width="12" height="14" rx="2" fill={engineColor} opacity="0.8" />
      {/* Smoke */}
      <circle cx="166" cy="46" r="5" fill={engineColor} opacity={engineAlloc > 30 ? 0.6 : 0.2} />
      <circle cx="162" cy="38" r="4" fill={engineColor} opacity={engineAlloc > 30 ? 0.4 : 0.1} />
      <circle cx="169" cy="31" r="3" fill={engineColor} opacity={engineAlloc > 30 ? 0.25 : 0.05} />

      {/* Mast */}
      <line x1="130" y1="30" x2="130" y2="90" stroke={GOLD} strokeWidth="2" />
      <line x1="100" y1="50" x2="160" y2="50" stroke={GOLD} strokeWidth="1.2" />

      {/* Flag */}
      <polygon points="130,30 155,40 130,50" fill={GOLD_LIGHT} opacity="0.9" />

      {/* Lifebuoy */}
      <circle cx="65" cy="115" r="12" fill="none" stroke={lifeColor} strokeWidth="3.5" filter="url(#glow)" />
      <circle cx="65" cy="115" r="6" fill={lifeColor} opacity="0.3" />
      <line x1="65" y1="103" x2="65" y2="108" stroke={lifeColor} strokeWidth="2" />
      <line x1="65" y1="122" x2="65" y2="127" stroke={lifeColor} strokeWidth="2" />
      <line x1="53" y1="115" x2="58" y2="115" stroke={lifeColor} strokeWidth="2" />
      <line x1="72" y1="115" x2="77" y2="115" stroke={lifeColor} strokeWidth="2" />

      {/* Engine glow */}
      <ellipse cx="166" cy="76" rx="16" ry="24" fill="url(#engineGlow)" />

      {/* Anchor */}
      <text x="210" y="138" fontSize="14" fill={GOLD} opacity="0.7">⚓</text>
    </svg>
  );
}

// ─── CUSTOM TOOLTIP ──────────────────────────────────────────────────────────
function CustomTooltip({ active, payload, label }) {
  if (!active || !payload?.length) return null;
  return (
    <div style={{ background: "#0D2137", border: `1px solid ${GOLD}40`, borderRadius: 10, padding: "10px 16px" }}>
      <p style={{ color: GOLD, fontFamily: "'Playfair Display', serif", marginBottom: 6, fontSize: 13 }}>{label}</p>
      {payload.map((p) => (
        <p key={p.name} style={{ color: p.color, fontSize: 12, margin: "2px 0", fontFamily: "monospace" }}>
          {p.name}: <b>${p.value?.toLocaleString()}</b>
        </p>
      ))}
    </div>
  );
}

// ─── MAIN COMPONENT ──────────────────────────────────────────────────────────
export default function TheGreatVoyage() {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);
  const [dragging, setDragging] = useState(false);
  const [fileName, setFileName] = useState(null);
  const fileRef = useRef();

  const parseFile = useCallback((file) => {
    setError(null);
    const reader = new FileReader();
    reader.onload = (e) => {
      try {
        const wb = XLSX.read(e.target.result, { type: "array" });

        // Validate sheets
        const missingSheets = [];
        if (!wb.SheetNames.includes("Fueling")) missingSheets.push("Fueling");
        if (!wb.SheetNames.includes("VesselParts")) missingSheets.push("VesselParts");
        if (!wb.SheetNames.includes("Target")) missingSheets.push("Target");
        if (missingSheets.length) {
          setError(`Sheet tidak ditemukan: ${missingSheets.join(", ")}. Gunakan template yang disediakan.`);
          return;
        }

        const fuelSheet = XLSX.utils.sheet_to_json(wb.Sheets["Fueling"]);
        const partsSheet = XLSX.utils.sheet_to_json(wb.Sheets["VesselParts"]);
        const targetSheet = XLSX.utils.sheet_to_json(wb.Sheets["Target"]);

        // Validate columns
        const fuelRow = fuelSheet[0] || {};
        const missingFuel = REQUIRED_FUEL_COLS.filter(c => !(c in fuelRow));
        if (missingFuel.length) { setError(`Kolom hilang di sheet Fueling: ${missingFuel.join(", ")}`); return; }

        const partRow = partsSheet[0] || {};
        const missingParts = REQUIRED_PARTS_COLS.filter(c => !(c in partRow));
        if (missingParts.length) { setError(`Kolom hilang di sheet VesselParts: ${missingParts.join(", ")}`); return; }

        const targetRow = targetSheet[0] || {};
        if (!("Target_Passive_Income" in targetRow)) { setError("Kolom Target_Passive_Income tidak ditemukan di sheet Target."); return; }

        const parts = partsSheet.map(r => ({
          Nama_Aset: r.Nama_Aset,
          Alokasi_Persen: Number(r.Alokasi_Persen),
          Return_Persen: Number(r.Return_Persen)
        }));

        const result = calculate(fuelRow, parts, targetRow);
        setData(result);
        setFileName(file.name);
      } catch (err) {
        setError("Gagal membaca file. Pastikan format Excel valid.");
      }
    };
    reader.readAsArrayBuffer(file);
  }, []);

  const handleDrop = useCallback((e) => {
    e.preventDefault();
    setDragging(false);
    const file = e.dataTransfer.files[0];
    if (file) parseFile(file);
  }, [parseFile]);

  const handleFileChange = (e) => {
    const file = e.target.files[0];
    if (file) parseFile(file);
  };

  // ── EMPTY STATE ─────────────────────────────────────────────────────────────
  if (!data) {
    return (
      <div style={{
        minHeight: "100vh", background: NAVY,
        fontFamily: "'Georgia', 'Times New Roman', serif",
        display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center",
        padding: "40px 20px", position: "relative", overflow: "hidden"
      }}>
        {/* Background decoration */}
        <div style={{
          position: "absolute", inset: 0, opacity: 0.04,
          backgroundImage: `radial-gradient(circle at 20% 50%, ${GOLD} 0%, transparent 50%),
                            radial-gradient(circle at 80% 20%, ${TEAL} 0%, transparent 40%)`,
          pointerEvents: "none"
        }} />

        {/* Compass decoration */}
        <div style={{ fontSize: 56, marginBottom: 8, filter: `drop-shadow(0 0 20px ${GOLD}60)` }}>🧭</div>

        <h1 style={{
          fontFamily: "'Playfair Display', 'Georgia', serif",
          color: GOLD_LIGHT, fontSize: "clamp(28px, 5vw, 48px)",
          textAlign: "center", margin: "0 0 8px",
          textShadow: `0 0 40px ${GOLD}50`, letterSpacing: "0.05em"
        }}>
          The Great Voyage
        </h1>
        <p style={{ color: "#7A9AB5", fontSize: 15, textAlign: "center", marginBottom: 48, maxWidth: 420, lineHeight: 1.7 }}>
          Navigasi menuju kebebasan finansial. Upload Logbook Excel-mu untuk memulai pelayaran.
        </p>

        {/* Drop Zone */}
        <div
          onDragOver={(e) => { e.preventDefault(); setDragging(true); }}
          onDragLeave={() => setDragging(false)}
          onDrop={handleDrop}
          onClick={() => fileRef.current?.click()}
          style={{
            width: "100%", maxWidth: 420, border: `2px dashed ${dragging ? GOLD : "#2A4A6B"}`,
            borderRadius: 16, padding: "48px 32px", textAlign: "center", cursor: "pointer",
            background: dragging ? `${GOLD}08` : `${NAVY2}80`,
            transition: "all 0.3s ease",
            boxShadow: dragging ? `0 0 40px ${GOLD}30` : "none"
          }}
        >
          <Upload size={36} color={dragging ? GOLD : "#4A7A9B"} style={{ marginBottom: 16, display: "block", margin: "0 auto 16px" }} />
          <p style={{ color: dragging ? GOLD_LIGHT : "#7A9AB5", fontSize: 15, margin: 0 }}>
            {dragging ? "Lepaskan untuk upload..." : "Drag & drop file Excel di sini, atau klik untuk memilih"}
          </p>
          <p style={{ color: "#3A6A8A", fontSize: 12, marginTop: 8 }}>Mendukung: .xlsx, .xls</p>
        </div>
        <input ref={fileRef} type="file" accept=".xlsx,.xls" onChange={handleFileChange} style={{ display: "none" }} />

        {/* Error */}
        {error && (
          <div style={{
            marginTop: 20, padding: "14px 20px", borderRadius: 10,
            background: `${RED}15`, border: `1px solid ${RED}50`,
            display: "flex", alignItems: "flex-start", gap: 10, maxWidth: 420, width: "100%"
          }}>
            <AlertTriangle size={18} color={RED} style={{ flexShrink: 0, marginTop: 2 }} />
            <p style={{ color: "#FCA5A5", fontSize: 13, margin: 0, lineHeight: 1.6 }}>{error}</p>
          </div>
        )}

        {/* Download Template */}
        <button
          onClick={downloadTemplate}
          style={{
            marginTop: 28, display: "flex", alignItems: "center", gap: 8,
            background: "transparent", border: `1px solid ${GOLD}60`,
            color: GOLD, padding: "12px 24px", borderRadius: 8, cursor: "pointer",
            fontSize: 14, fontFamily: "inherit", transition: "all 0.2s",
            letterSpacing: "0.05em"
          }}
          onMouseEnter={e => { e.currentTarget.style.background = `${GOLD}15`; e.currentTarget.style.borderColor = GOLD; }}
          onMouseLeave={e => { e.currentTarget.style.background = "transparent"; e.currentTarget.style.borderColor = `${GOLD}60`; }}
        >
          <Download size={16} />
          Download Template Logbook
        </button>
      </div>
    );
  }

  // ── DASHBOARD STATE ─────────────────────────────────────────────────────────
  const {
    annualFuel, annualSaving, weightedReturn, fireCapital,
    projectionData, contractCount, yearsToFIRE,
    parts, targetPI, on, off, gaji
  } = data;

  const fireYear = projectionData.findIndex(d => d.Investasi >= fireCapital);
  const fireReached = fireYear >= 0;

  const getColor = (idx) => {
    const colors = [GOLD, TEAL, "#A78BFA", "#F472B6", GREEN];
    return colors[idx % colors.length];
  };

  return (
    <div style={{
      minHeight: "100vh", background: NAVY,
      fontFamily: "'Georgia', 'Times New Roman', serif",
      color: "#C8D8E8", padding: "24px 16px"
    }}>
      {/* ── HEADER */}
      <div style={{ textAlign: "center", marginBottom: 32, position: "relative" }}>
        <p style={{ color: "#4A7A9B", fontSize: 12, letterSpacing: "0.2em", marginBottom: 4, textTransform: "uppercase" }}>
          Logbook: {fileName}
        </p>
        <h1 style={{
          fontFamily: "'Playfair Display', 'Georgia', serif",
          color: GOLD_LIGHT, fontSize: "clamp(22px, 4vw, 36px)",
          margin: 0, textShadow: `0 0 30px ${GOLD}40`
        }}>
          ⚓ The Great Voyage
        </h1>
        <button
          onClick={() => { setData(null); setError(null); setFileName(null); }}
          style={{
            position: "absolute", right: 0, top: "50%", transform: "translateY(-50%)",
            background: "transparent", border: `1px solid #2A4A6B`,
            color: "#4A7A9B", padding: "6px 14px", borderRadius: 6,
            cursor: "pointer", fontSize: 12, fontFamily: "inherit"
          }}
        >
          Ganti File
        </button>
      </div>

      <div style={{ maxWidth: 960, margin: "0 auto" }}>

        {/* ── ROW 1: VESSEL + STATUS */}
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20, marginBottom: 20 }}>

          {/* Vessel Visual */}
          <div style={{
            background: `${NAVY2}CC`, border: `1px solid ${GOLD}25`,
            borderRadius: 16, padding: "24px 16px", display: "flex",
            flexDirection: "column", alignItems: "center"
          }}>
            <p style={{ color: GOLD, fontSize: 12, letterSpacing: "0.15em", textTransform: "uppercase", marginBottom: 12, margin: "0 0 12px" }}>
              Armada Investasi
            </p>
            <VesselSVG parts={parts} />
            <div style={{ width: "100%", marginTop: 16, display: "flex", flexDirection: "column", gap: 6 }}>
              {parts.map((p, i) => (
                <div key={i} style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
                  <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
                    <div style={{ width: 10, height: 10, borderRadius: "50%", background: getColor(i), boxShadow: `0 0 6px ${getColor(i)}` }} />
                    <span style={{ fontSize: 12, color: "#8AAABF" }}>{p.Nama_Aset}</span>
                  </div>
                  <span style={{ fontSize: 12, color: getColor(i), fontFamily: "monospace" }}>
                    {p.Alokasi_Persen}% @ {p.Return_Persen}%
                  </span>
                </div>
              ))}
            </div>
          </div>

          {/* Status Panel */}
          <div style={{ display: "flex", flexDirection: "column", gap: 14 }}>
            {/* FIRE Status */}
            <div style={{
              background: fireReached ? `${GREEN}10` : `${GOLD}08`,
              border: `1px solid ${fireReached ? GREEN : GOLD}40`,
              borderRadius: 14, padding: "18px 20px", flex: 1
            }}>
              <p style={{ color: "#6A9AB5", fontSize: 11, textTransform: "uppercase", letterSpacing: "0.15em", margin: "0 0 6px" }}>
                Sisa Perjalanan
              </p>
              <p style={{
                fontFamily: "'Playfair Display', serif",
                color: fireReached ? GREEN : GOLD_LIGHT,
                fontSize: "clamp(24px, 4vw, 36px)", margin: "0 0 4px",
                textShadow: `0 0 20px ${fireReached ? GREEN : GOLD}50`
              }}>
                {contractCount} Kontrak
              </p>
              <p style={{ color: "#6A9AB5", fontSize: 13, margin: 0 }}>
                ≈ {yearsToFIRE.toFixed(1)} tahun menuju FIRE
              </p>
            </div>

            {/* Key Metrics */}
            {[
              { label: "Annual Fuel (Tabungan/Thn)", value: `$${annualFuel.toLocaleString()}`, color: GOLD },
              { label: "Modal FIRE (Target × 25)", value: `$${fireCapital.toLocaleString()}`, color: TEAL },
              { label: "Weighted Return", value: `${(weightedReturn * 100).toFixed(2)}%`, color: "#A78BFA" },
              { label: "Target Passive Income/Bln", value: `$${targetPI.toLocaleString()}`, color: GREEN },
            ].map((m, i) => (
              <div key={i} style={{
                background: `${NAVY2}CC`, border: `1px solid #1A3A5A`,
                borderRadius: 10, padding: "12px 16px",
                display: "flex", justifyContent: "space-between", alignItems: "center"
              }}>
                <span style={{ fontSize: 12, color: "#6A9AB5" }}>{m.label}</span>
                <span style={{ fontFamily: "monospace", fontWeight: "bold", color: m.color, fontSize: 15 }}>{m.value}</span>
              </div>
            ))}
          </div>
        </div>

        {/* ── ROW 2: CONTRACT STATS */}
        <div style={{
          display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: 14, marginBottom: 20
        }}>
          {[
            { icon: "⚡", label: "Bulan On-Board", value: `${on} bln`, sub: "per kontrak" },
            { icon: "🏠", label: "Bulan Off-Board", value: `${off} bln`, sub: "per kontrak" },
            { icon: "💰", label: "Gaji Laut/Bln", value: `$${Number(gaji).toLocaleString()}`, sub: "gross" },
          ].map((s, i) => (
            <div key={i} style={{
              background: `${NAVY2}CC`, border: `1px solid ${GOLD}20`,
              borderRadius: 12, padding: "16px", textAlign: "center"
            }}>
              <div style={{ fontSize: 22, marginBottom: 8 }}>{s.icon}</div>
              <p style={{ color: "#6A9AB5", fontSize: 11, textTransform: "uppercase", letterSpacing: "0.1em", margin: "0 0 4px" }}>{s.label}</p>
              <p style={{ fontFamily: "monospace", color: GOLD_LIGHT, fontSize: 20, margin: "0 0 2px", fontWeight: "bold" }}>{s.value}</p>
              <p style={{ color: "#4A6A7A", fontSize: 11, margin: 0 }}>{s.sub}</p>
            </div>
          ))}
        </div>

        {/* ── ROW 3: PROJECTION CHART */}
        <div style={{
          background: `${NAVY2}CC`, border: `1px solid ${GOLD}25`,
          borderRadius: 16, padding: "24px 16px 16px", marginBottom: 20
        }}>
          <p style={{ color: GOLD, fontSize: 12, letterSpacing: "0.15em", textTransform: "uppercase", margin: "0 0 20px", paddingLeft: 8 }}>
            Proyeksi Pelayaran — Jalur Investasi vs Gaji Saja
          </p>
          <ResponsiveContainer width="100%" height={260}>
            <AreaChart data={projectionData.filter((_, i) => i % 2 === 0 || i === projectionData.length - 1)} margin={{ top: 10, right: 10, left: 0, bottom: 0 }}>
              <defs>
                <linearGradient id="gradInv" x1="0" y1="0" x2="0" y2="1">
                  <stop offset="5%" stopColor={GOLD} stopOpacity={0.3} />
                  <stop offset="95%" stopColor={GOLD} stopOpacity={0} />
                </linearGradient>
                <linearGradient id="gradSal" x1="0" y1="0" x2="0" y2="1">
                  <stop offset="5%" stopColor={TEAL} stopOpacity={0.2} />
                  <stop offset="95%" stopColor={TEAL} stopOpacity={0} />
                </linearGradient>
              </defs>
              <CartesianGrid strokeDasharray="3 3" stroke="#1A3A5A" />
              <XAxis dataKey="year" tick={{ fill: "#4A7A9B", fontSize: 11 }} axisLine={false} tickLine={false} />
              <YAxis tick={{ fill: "#4A7A9B", fontSize: 10 }} axisLine={false} tickLine={false}
                tickFormatter={v => v >= 1000000 ? `$${(v / 1000000).toFixed(1)}M` : `$${(v / 1000).toFixed(0)}K`} />
              <Tooltip content={<CustomTooltip />} />
              <Legend wrapperStyle={{ color: "#8AAABF", fontSize: 12 }} />
              <Area type="monotone" dataKey="GajiSaja" name="Jalur Gaji Saja" stroke={TEAL} fill="url(#gradSal)" strokeWidth={2} dot={false} strokeDasharray="5 3" />
              <Area type="monotone" dataKey="Investasi" name="Jalur Investasi" stroke={GOLD} fill="url(#gradInv)" strokeWidth={2.5} dot={false} />
              {fireReached && (
                <Area type="monotone" dataKey="FIRE" name="Target FIRE" stroke={RED} fill="none" strokeWidth={1.5} strokeDasharray="4 4" dot={false} />
              )}
            </AreaChart>
          </ResponsiveContainer>
          {fireReached && (
            <p style={{ textAlign: "center", color: GREEN, fontSize: 13, marginTop: 12, fontFamily: "inherit" }}>
              🎯 FIRE tercapai di sekitar <b>Tahun {fireYear + 1}</b> dengan jalur investasi
            </p>
          )}
        </div>

        {/* ── ROW 4: ASSET ALLOCATION TABLE */}
        <div style={{
          background: `${NAVY2}CC`, border: `1px solid ${GOLD}25`,
          borderRadius: 16, padding: "20px"
        }}>
          <p style={{ color: GOLD, fontSize: 12, letterSpacing: "0.15em", textTransform: "uppercase", margin: "0 0 16px" }}>
            Manifest Aset — Vessel Parts
          </p>
          <table style={{ width: "100%", borderCollapse: "collapse", fontSize: 13 }}>
            <thead>
              <tr>
                {["Nama Aset", "Alokasi", "Return/Thn", "Annual Fuel → Aset"].map(h => (
                  <th key={h} style={{ textAlign: "left", color: "#4A7A9B", fontWeight: "normal", paddingBottom: 10, fontSize: 11, textTransform: "uppercase", letterSpacing: "0.1em", borderBottom: `1px solid #1A3A5A` }}>{h}</th>
                ))}
              </tr>
            </thead>
            <tbody>
              {parts.map((p, i) => {
                const allocated = annualSaving * (p.Alokasi_Persen / 100);
                return (
                  <tr key={i} style={{ borderBottom: `1px solid #1A3A5A22` }}>
                    <td style={{ padding: "10px 0", display: "flex", alignItems: "center", gap: 8 }}>
                      <div style={{ width: 8, height: 8, borderRadius: "50%", background: getColor(i), flexShrink: 0 }} />
                      <span style={{ color: "#C8D8E8" }}>{p.Nama_Aset}</span>
                    </td>
                    <td style={{ color: getColor(i), fontFamily: "monospace" }}>{p.Alokasi_Persen}%</td>
                    <td style={{ color: "#8AAABF", fontFamily: "monospace" }}>{p.Return_Persen}%</td>
                    <td style={{ color: GOLD_LIGHT, fontFamily: "monospace" }}>${allocated.toLocaleString(undefined, { maximumFractionDigits: 0 })}/thn</td>
                  </tr>
                );
              })}
            </tbody>
          </table>
        </div>

        {/* Footer */}
        <p style={{ textAlign: "center", color: "#2A4A6A", fontSize: 11, marginTop: 24, letterSpacing: "0.1em" }}>
          THE GREAT VOYAGE · SEAFARER WEALTH NAVIGATOR · DATA DRIVEN BY YOUR LOGBOOK
        </p>
      </div>
    </div>
  );
}
