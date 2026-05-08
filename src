import { useState, useCallback, useEffect } from "react";

const TEAL = "#0D5C63";
const TEAL_LIGHT = "#1A7A83";
const TEAL_PALE = "#E8F4F5";
const GOLD = "#C9963A";
const GRAY_100 = "#F4F4F2";
const GRAY_200 = "#E5E5E5";
const GRAY_400 = "#9E9E9E";
const GRAY_600 = "#5A5A5A";
const GRAY_800 = "#2C2C2C";
const DANGER = "#C0392B";
const DANGER_LIGHT = "#FDECEA";
const SUCCESS = "#1E7E5A";

const SECTIONS = [
  { id: "control",    name: "Control",        icon: "📋" },
  { id: "datos",      name: "Datos",          icon: "👤" },
  { id: "heredofam",  name: "Heredo-fam.",    icon: "👨‍👩‍👧" },
  { id: "patol",      name: "Patológicos",    icon: "🏥" },
  { id: "nopatol",    name: "No Patológicos", icon: "🍃" },
  { id: "explor",     name: "Exploración",    icon: "🔍" },
  { id: "dolor",      name: "Dolor",          icon: "📊" },
  { id: "tratActual", name: "Tratamiento",    icon: "💊" },
  { id: "dx",         name: "Diagnóstico",    icon: "🩺" },
  { id: "plan",       name: "Plan",           icon: "📝" },
  { id: "observ",     name: "Observaciones",  icon: "💬" },
  { id: "validacion", name: "Validación",     icon: "✅" },
];

const PAIN_COLORS = ["#4CAF50","#66BB6A","#9CCC65","#D4E157","#FFEE58","#FFA726","#FF7043","#EF5350","#E53935","#C62828","#B71C1C"];
const PAIN_LABELS = ["Sin dolor","Muy leve","Leve","Leve-mod.","Moderado","Moderado","Mod.-severo","Severo","Severo","Muy severo","Insoportable"];

const today = () => new Date().toLocaleDateString("es-MX");
const nowTime = () => new Date().toLocaleTimeString("es-MX", { hour: "2-digit", minute: "2-digit" });

// ─── UI COMPONENTS ───────────────────────────────────────────────────

function Input({ label, value, onChange, placeholder = "", type = "text", required }) {
  return (
    <div style={{ marginBottom: 16 }}>
      {label && (
        <div style={{ fontSize: 11, fontWeight: 700, letterSpacing: ".6px", textTransform: "uppercase", color: GRAY_600, marginBottom: 7 }}>
          {label}{required && <span style={{ color: DANGER }}> *</span>}
        </div>
      )}
      <input
        type={type}
        value={value || ""}
        onChange={e => onChange(e.target.value)}
        placeholder={placeholder}
        inputMode={type === "number" ? "numeric" : type === "tel" ? "tel" : "text"}
        style={{
          width: "100%", padding: "13px 14px", border: `2px solid ${GRAY_200}`,
          borderRadius: 10, fontSize: 16, fontFamily: "inherit", color: GRAY_800,
          background: "white", outline: "none", boxSizing: "border-box",
          WebkitAppearance: "none",
        }}
        onFocus={e => e.target.style.borderColor = TEAL}
        onBlur={e => e.target.style.borderColor = GRAY_200}
      />
    </div>
  );
}

function Textarea({ label, value, onChange, placeholder = "", rows = 3 }) {
  return (
    <div style={{ marginBottom: 16 }}>
      {label && (
        <div style={{ fontSize: 11, fontWeight: 700, letterSpacing: ".6px", textTransform: "uppercase", color: GRAY_600, marginBottom: 7 }}>
          {label}
        </div>
      )}
      <textarea
        value={value || ""}
        onChange={e => onChange(e.target.value)}
        placeholder={placeholder}
        rows={rows}
        style={{
          width: "100%", padding: "13px 14px", border: `2px solid ${GRAY_200}`,
          borderRadius: 10, fontSize: 16, fontFamily: "inherit", color: GRAY_800,
          background: "white", outline: "none", resize: "none", lineHeight: 1.6,
          boxSizing: "border-box",
        }}
        onFocus={e => e.target.style.borderColor = TEAL}
        onBlur={e => e.target.style.borderColor = GRAY_200}
      />
    </div>
  );
}

function ToggleGroup({ label, value, onChange, options, cols }) {
  return (
    <div style={{ marginBottom: 16 }}>
      {label && <div style={{ fontSize: 11, fontWeight: 700, letterSpacing: ".6px", textTransform: "uppercase", color: GRAY_600, marginBottom: 7 }}>{label}</div>}
      <div style={{ display: "grid", gridTemplateColumns: `repeat(${cols || options.length}, 1fr)`, gap: 8 }}>
        {options.map(o => (
          <button
            key={o.v}
            onClick={() => onChange(o.v)}
            style={{
              padding: "13px 8px", border: `2px solid ${value === o.v ? TEAL : GRAY_200}`,
              borderRadius: 10, background: value === o.v ? TEAL : "white",
              color: value === o.v ? "white" : GRAY_600,
              fontSize: 14, fontWeight: 600, cursor: "pointer", fontFamily: "inherit",
              transition: "all .15s",
            }}
          >{o.l}</button>
        ))}
      </div>
    </div>
  );
}

function YesNo({ label, value, onChange, detail, onDetailChange }) {
  return (
    <div style={{ marginBottom: 14 }}>
      <div style={{ display: "flex", alignItems: "center", gap: 10, flexWrap: "wrap", marginBottom: value === "si" ? 8 : 0 }}>
        <span style={{ flex: 1, fontSize: 15, fontWeight: 500, color: GRAY_800, minWidth: 150 }}>{label}</span>
        <div style={{ display: "flex", gap: 8 }}>
          {["si", "no"].map(v => (
            <button
              key={v}
              onClick={() => onChange(v)}
              style={{
                padding: "8px 20px", border: `2px solid ${value === v ? (v === "si" ? SUCCESS : GRAY_600) : GRAY_200}`,
                borderRadius: 50, background: value === v ? (v === "si" ? SUCCESS : GRAY_600) : "white",
                color: value === v ? "white" : GRAY_600,
                fontSize: 14, fontWeight: 700, cursor: "pointer", fontFamily: "inherit",
              }}
            >{v === "si" ? "Sí" : "No"}</button>
          ))}
        </div>
      </div>
      {value === "si" && detail !== undefined && (
        <textarea
          value={detail || ""}
          onChange={e => onDetailChange(e.target.value)}
          placeholder="Detalla aquí..."
          rows={2}
          style={{
            width: "100%", padding: "10px 14px", border: `2px solid ${TEAL}`,
            borderRadius: 10, fontSize: 15, fontFamily: "inherit", background: TEAL_PALE,
            outline: "none", resize: "none", boxSizing: "border-box",
          }}
        />
      )}
    </div>
  );
}

function CheckGrid({ label, value = [], onChange, options }) {
  const toggle = v => onChange(value.includes(v) ? value.filter(x => x !== v) : [...value, v]);
  return (
    <div style={{ marginBottom: 16 }}>
      {label && <div style={{ fontSize: 11, fontWeight: 700, letterSpacing: ".6px", textTransform: "uppercase", color: GRAY_600, marginBottom: 7 }}>{label}</div>}
      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 8 }}>
        {options.map(o => {
          const checked = value.includes(o);
          return (
            <button
              key={o}
              onClick={() => toggle(o)}
              style={{
                display: "flex", alignItems: "center", gap: 10,
                padding: "13px 14px", border: `2px solid ${checked ? TEAL : GRAY_200}`,
                borderRadius: 10, background: checked ? TEAL_PALE : "white",
                cursor: "pointer", textAlign: "left", fontFamily: "inherit",
              }}
            >
              <div style={{
                width: 22, height: 22, borderRadius: 6, border: `2px solid ${checked ? TEAL : GRAY_400}`,
                background: checked ? TEAL : "white", display: "flex", alignItems: "center", justifyContent: "center",
                flexShrink: 0, color: "white", fontSize: 13, fontWeight: 700,
              }}>
                {checked ? "✓" : ""}
              </div>
              <span style={{ fontSize: 14, fontWeight: 500, color: checked ? TEAL : GRAY_800 }}>{o}</span>
            </button>
          );
        })}
      </div>
    </div>
  );
}

function Subsection({ title, children }) {
  return (
    <div style={{ borderLeft: `3px solid #C5E4E7`, paddingLeft: 16, marginBottom: 24 }}>
      <div style={{ fontSize: 12, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".6px", color: TEAL, marginBottom: 14 }}>{title}</div>
      {children}
    </div>
  );
}

function SectionHeader({ num, title, desc }) {
  return (
    <div style={{ marginBottom: 24 }}>
      <div style={{ display: "inline-block", background: TEAL_PALE, color: TEAL, fontSize: 11, fontWeight: 700, padding: "4px 12px", borderRadius: 50, marginBottom: 8, letterSpacing: ".6px", textTransform: "uppercase" }}>
        Sección {num}
      </div>
      <div style={{ fontSize: 26, fontWeight: 700, color: GRAY_800, lineHeight: 1.2 }}>{title}</div>
      {desc && <div style={{ fontSize: 14, color: GRAY_400, marginTop: 5, fontWeight: 300 }}>{desc}</div>}
    </div>
  );
}

// ─── SECTION RENDERERS ───────────────────────────────────────────────

function S1({ f, set }) {
  return <>
    <SectionHeader num={1} title="Control de Consulta" desc="Datos de identificación del expediente" />
    <Input label="Folio" value={f.folio} onChange={v => set("folio", v)} placeholder="Ej. 0001" />
    <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
      <Input label="Fecha" value={f.fecha} onChange={v => set("fecha", v)} placeholder="DD/MM/AAAA" />
      <Input label="Hora" value={f.hora} onChange={v => set("hora", v)} placeholder="00:00" />
    </div>
  </>;
}

function S2({ f, set }) {
  return <>
    <SectionHeader num={2} title="Datos Generales" desc="Información del paciente" />
    <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
      <Input label="Apellido paterno *" value={f.apellidoP} onChange={v => set("apellidoP", v)} />
      <Input label="Apellido materno" value={f.apellidoM} onChange={v => set("apellidoM", v)} />
    </div>
    <Input label="Nombre(s) *" value={f.nombre} onChange={v => set("nombre", v)} />
    <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
      <Input label="Edad" value={f.edad} onChange={v => set("edad", v)} type="number" placeholder="años" />
      <Input label="Fecha de nacimiento" value={f.fechaNac} onChange={v => set("fechaNac", v)} placeholder="DD/MM/AAAA" />
    </div>
    <ToggleGroup label="Sexo" value={f.sexo} onChange={v => set("sexo", v)} options={[{l:"Femenino",v:"F"},{l:"Masculino",v:"M"}]} />
    <ToggleGroup label="Estado civil" value={f.estadoCivil} onChange={v => set("estadoCivil", v)}
      options={[{l:"Soltero/a",v:"soltero"},{l:"Casado/a",v:"casado"},{l:"Divorciado/a",v:"divorciado"},{l:"Viudo/a",v:"viudo"}]} cols={2} />
    <div style={{ height: 1, background: GRAY_200, margin: "16px 0" }} />
    <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
      <Input label="Calle" value={f.calle} onChange={v => set("calle", v)} />
      <Input label="Número" value={f.numero} onChange={v => set("numero", v)} />
      <Input label="Colonia" value={f.colonia} onChange={v => set("colonia", v)} />
      <Input label="C.P." value={f.cp} onChange={v => set("cp", v)} type="number" />
      <Input label="Ciudad" value={f.ciudad} onChange={v => set("ciudad", v)} />
      <Input label="Estado" value={f.estadoDir} onChange={v => set("estadoDir", v)} />
      <Input label="Tel. particular" value={f.telPart} onChange={v => set("telPart", v)} type="tel" />
      <Input label="Tel. móvil" value={f.telMovil} onChange={v => set("telMovil", v)} type="tel" />
      <Input label="Ocupación" value={f.ocupacion} onChange={v => set("ocupacion", v)} />
      <Input label="Escolaridad" value={f.escolaridad} onChange={v => set("escolaridad", v)} />
    </div>
  </>;
}

function FamilyBlock({ title, fkey, f, set }) {
  return (
    <Subsection title={title}>
      <ToggleGroup value={f[fkey+"_estado"]} onChange={v => set(fkey+"_estado", v)}
        options={[{l:"Vivo/a",v:"vivo"},{l:"Finado/a",v:"finado"}]} />
      <Textarea value={f[fkey+"_enf"]} onChange={v => set(fkey+"_enf", v)}
        placeholder="Enfermedades que padece / padeció..." />
      {f[fkey+"_estado"] === "finado" && (
        <Input label="Causa de fallecimiento" value={f[fkey+"_causa"]} onChange={v => set(fkey+"_causa", v)} />
      )}
    </Subsection>
  );
}

function S3({ f, set }) {
  return <>
    <SectionHeader num={3} title="Antecedentes Heredofamiliares" desc="Estado y padecimientos de familiares directos" />
    <FamilyBlock title="Padre" fkey="padre" f={f} set={set} />
    <FamilyBlock title="Madre" fkey="madre" f={f} set={set} />
    <FamilyBlock title="Hijo/a(s)" fkey="hijos" f={f} set={set} />
    <FamilyBlock title="Abuelo/a(s)" fkey="abuelos" f={f} set={set} />
  </>;
}

function S4({ f, set }) {
  return <>
    <SectionHeader num={4} title="Antecedentes Patológicos" desc="Antecedentes de importancia clínica" />
    <Subsection title="Alergias">
      <YesNo label="Alergias quirúrgicas" value={f.alQuir} onChange={v => set("alQuir", v)} detail={f.alQuirD} onDetailChange={v => set("alQuirD", v)} />
      <YesNo label="Alergias médicas" value={f.alMed} onChange={v => set("alMed", v)} detail={f.alMedD} onDetailChange={v => set("alMedD", v)} />
      <YesNo label="Alergias estéticas" value={f.alEst} onChange={v => set("alEst", v)} detail={f.alEstD} onDetailChange={v => set("alEstD", v)} />
      <Input label="Otras alergias" value={f.alOtras} onChange={v => set("alOtras", v)} placeholder="Especifica..." />
    </Subsection>
    <Subsection title="Procedimientos / Antecedentes Relevantes">
      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
        <Input label="Núm. procedimientos" value={f.numProc} onChange={v => set("numProc", v)} type="number" />
        <Input label="Fecha último" value={f.fechaProc} onChange={v => set("fechaProc", v)} placeholder="DD/MM/AAAA" />
      </div>
      <YesNo label="Cardiacos" value={f.cardiacos} onChange={v => set("cardiacos", v)} detail={f.cardiacosD} onDetailChange={v => set("cardiacosD", v)} />
      <YesNo label="Vasculares" value={f.vasculares} onChange={v => set("vasculares", v)} detail={f.vascularesD} onDetailChange={v => set("vascularesD", v)} />
      <YesNo label="Óseos" value={f.oseos} onChange={v => set("oseos", v)} detail={f.oseosD} onDetailChange={v => set("oseosD", v)} />
      <YesNo label="Diabetes" value={f.diabetes} onChange={v => set("diabetes", v)} detail={f.diabetesD} onDetailChange={v => set("diabetesD", v)} />
      <YesNo label="Hipertensión arterial" value={f.hipertension} onChange={v => set("hipertension", v)} detail={f.hipertensionD} onDetailChange={v => set("hipertensionD", v)} />
      <YesNo label="Transfusiones" value={f.transfusiones} onChange={v => set("transfusiones", v)} detail={f.transfusionesD} onDetailChange={v => set("transfusionesD", v)} />
      <Textarea label="Otros antecedentes" value={f.otrosAntec} onChange={v => set("otrosAntec", v)} placeholder="Describe..." />
    </Subsection>
  </>;
}

function S5({ f, set }) {
  return <>
    <SectionHeader num={5} title="Antecedentes No Patológicos" />
    <ToggleGroup label="Tabaquismo" value={f.tabaquismo} onChange={v => set("tabaquismo", v)}
      options={[{l:"Fumador",v:"si"},{l:"Ex-fumador",v:"ex"},{l:"No fuma",v:"no"}]} />
    <ToggleGroup label="Ingesta de alcohol" value={f.alcohol} onChange={v => set("alcohol", v)}
      options={[{l:"Cada semana",v:"semana"},{l:"Una vez al mes",v:"mes"},{l:"Nunca",v:"nunca"}]} />
    <ToggleGroup label="Vacunas al día" value={f.vacunas} onChange={v => set("vacunas", v)}
      options={[{l:"Sí",v:"si"},{l:"Parcial",v:"parcial"},{l:"No",v:"no"}]} />
    <YesNo label="¿Usa medicamentos / estimulantes no recetados?" value={f.medicNR} onChange={v => set("medicNR", v)} detail={f.medicNRD} onDetailChange={v => set("medicNRD", v)} />
    <Textarea label="Otros" value={f.otrosNoPatol} onChange={v => set("otrosNoPatol", v)} placeholder="Especifica..." />
  </>;
}

function S6({ f, set }) {
  return <>
    <SectionHeader num={6} title="Exploración Física" desc="Observaciones de movilidad y traslado" />
    <CheckGrid label="Marcha" value={f.marcha} onChange={v => set("marcha", v)}
      options={["Libre","Espástica","Claudicante","Atáxica","Con ayuda"]} />
    {(f.marcha || []).includes("Con ayuda") && (
      <Input label="Especificar ayuda para marcha" value={f.marchaAyuda} onChange={v => set("marchaAyuda", v)} placeholder="Bastón, andadera, muletas..." />
    )}
    <CheckGrid label="Traslados" value={f.traslados} onChange={v => set("traslados", v)}
      options={["Independiente","Silla de ruedas","Con ayudas","Camilla"]} />
    <Textarea label="Observaciones adicionales" value={f.explorObs} onChange={v => set("explorObs", v)} placeholder="Notas de exploración..." />
  </>;
}

function S7({ f, set }) {
  const nivel = parseInt(f.dolor ?? 0);
  return <>
    <SectionHeader num={7} title="Escala Visual de Dolor" desc="Marca el nivel de dolor del paciente" />
    <div style={{ textAlign: "center", marginBottom: 24 }}>
      <div style={{ fontSize: 72, fontWeight: 800, color: PAIN_COLORS[nivel], lineHeight: 1, fontVariantNumeric: "tabular-nums" }}>{nivel}</div>
      <div style={{ fontSize: 15, color: GRAY_600, marginTop: 6 }}>{PAIN_LABELS[nivel]}</div>
    </div>
    <input
      type="range" min={0} max={10} value={nivel}
      onChange={e => set("dolor", parseInt(e.target.value))}
      style={{ width: "100%", height: 8, borderRadius: 99, cursor: "pointer",
        accentColor: PAIN_COLORS[nivel], marginBottom: 8 }}
    />
    <div style={{ display: "flex", justifyContent: "space-between", fontSize: 11, color: GRAY_400, marginBottom: 16 }}>
      <span>0 — Sin dolor</span><span>10 — Insoportable</span>
    </div>
    <div style={{ display: "flex", gap: 6, justifyContent: "space-between" }}>
      {Array.from({ length: 11 }, (_, i) => (
        <button
          key={i}
          onClick={() => set("dolor", i)}
          style={{
            width: 34, height: 34, borderRadius: "50%", border: `2px solid ${nivel === i ? PAIN_COLORS[i] : GRAY_200}`,
            background: nivel === i ? PAIN_COLORS[i] : "white",
            color: nivel === i ? "white" : GRAY_600,
            fontSize: 12, fontWeight: 700, cursor: "pointer", fontFamily: "inherit",
            transition: "all .12s",
          }}
        >{i}</button>
      ))}
    </div>
  </>;
}

function S8({ f, set }) {
  return <>
    <SectionHeader num={8} title="Tratamiento Actual" desc="Tratamiento actual o previamente realizado" />
    <Textarea value={f.tratActual} onChange={v => set("tratActual", v)}
      placeholder="Describe medicamentos, dosis, frecuencia, duración..." rows={6} />
  </>;
}

function S9({ f, set }) {
  return <>
    <SectionHeader num={9} title="Diagnóstico(s)" />
    <Textarea value={f.diagnostico} onChange={v => set("diagnostico", v)}
      placeholder="Escribe el o los diagnósticos..." rows={6} />
  </>;
}

function S10({ f, set }) {
  return <>
    <SectionHeader num={10} title="Plan de Tratamiento" desc="Objetivos, prioridades y métodos" />
    <Textarea label="Objetivos" value={f.planObj} onChange={v => set("planObj", v)} placeholder="Objetivos del tratamiento..." rows={3} />
    <Textarea label="Prioridades" value={f.planPrio} onChange={v => set("planPrio", v)} placeholder="Prioridades..." rows={3} />
    <Textarea label="Métodos y técnicas de intervención" value={f.planMetodos} onChange={v => set("planMetodos", v)} placeholder="Describe los métodos y técnicas..." rows={3} />
  </>;
}

function S11({ f, set }) {
  return <>
    <SectionHeader num={11} title="Observaciones Clínicas" desc="Notas y observaciones del profesional" />
    <Textarea value={f.observaciones} onChange={v => set("observaciones", v)}
      placeholder="Observaciones clínicas..." rows={8} />
  </>;
}

function S12({ f, set }) {
  return <>
    <SectionHeader num={12} title="Validación del Expediente" desc="Información de cierre" />
    <Input label="Profesional responsable" value={f.profesional} onChange={v => set("profesional", v)} placeholder="Nombre completo" />
    <Input label="Cédula / N° de registro" value={f.cedula} onChange={v => set("cedula", v)} />
    <Input label="Fecha de cierre" value={f.fechaCierre} onChange={v => set("fechaCierre", v)} placeholder="DD/MM/AAAA" />
    <Textarea label="Firma / Vo. Bo." value={f.firma} onChange={v => set("firma", v)} rows={2} />
    <div style={{ marginTop: 24, padding: "24px 20px", background: TEAL_PALE, borderRadius: 14, textAlign: "center" }}>
      <div style={{ fontSize: 36, marginBottom: 8 }}>✅</div>
      <div style={{ fontSize: 20, fontWeight: 700, color: TEAL }}>Lista para guardar</div>
      <div style={{ fontSize: 13, color: GRAY_400, marginTop: 4 }}>Revisa los datos antes de confirmar</div>
    </div>
  </>;
}

const SECTION_COMPONENTS = [S1, S2, S3, S4, S5, S6, S7, S8, S9, S10, S11, S12];

// ─── MAIN APP ──────────────────────────────────────────────────────────

export default function App() {
  const [screen, setScreen] = useState("list");
  const [patients, setPatients] = useState(() => {
    const saved = localStorage.getItem("hc_patients_v1");
    return saved ? JSON.parse(saved) : [];
  });
  const [currentIdx, setCurrentIdx] = useState(0);
  const [form, setForm] = useState({});
  const [detailId, setDetailId] = useState(null);
  const [toast, setToast] = useState(null);

  // Save patients to localStorage whenever they change
  useEffect(() => {
    localStorage.setItem("hc_patients_v1", JSON.stringify(patients));
  }, [patients]);

  const showToast = (msg, type = "") => {
    setToast({ msg, type });
    setTimeout(() => setToast(null), 2600);
  };

  const setField = useCallback((key, val) => {
    setForm(prev => ({ ...prev, [key]: val }));
  }, []);

  const startNew = () => {
    setForm({ fecha: today(), hora: nowTime() });
    setCurrentIdx(0);
    setScreen("form");
  };

  const savePatient = () => {
    if (!form.nombre && !form.apellidoP) {
      showToast("⚠️ Ingresa al menos nombre o apellido");
      return;
    }
    const p = { id: Date.now(), savedAt: new Date().toISOString(), ...form };
    setPatients(prev => [p, ...prev]);
    showToast("✅ Historia guardada", "success");
    setTimeout(() => setScreen("list"), 700);
  };

  const deletePatient = id => {
    setPatients(prev => prev.filter(p => p.id !== id));
    setScreen("list");
    showToast("Registro eliminado");
  };

  const patientName = p => [p.apellidoP, p.apellidoM, p.nombre].filter(Boolean).join(" ") || "Sin nombre";

  // ── LIST SCREEN ──
  if (screen === "list") {
    const todayStr = today();
    const monthNow = new Date().getMonth();
    const todayCount = patients.filter(p => new Date(p.savedAt).toLocaleDateString("es-MX") === todayStr).length;
    const monthCount = patients.filter(p => new Date(p.savedAt).getMonth() === monthNow).length;

    return (
      <div style={{ minHeight: "100vh", background: GRAY_100, fontFamily: "system-ui, -apple-system, sans-serif" }}>
        {/* header */}
        <div style={{ background: TEAL, padding: "18px 20px", display: "flex", alignItems: "center", justifyContent: "space-between", position: "sticky", top: 0, zIndex: 10, paddingTop: "max(18px, env(safe-area-inset-top))" }}>
          <div style={{ display: "flex", alignItems: "center", gap: 12 }}>
            <div style={{ width: 38, height: 38, background: GOLD, borderRadius: 10, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 20 }}>🩺</div>
            <div>
              <div style={{ fontSize: 18, fontWeight: 700, color: "white" }}>Historia Clínica</div>
              <div style={{ fontSize: 11, color: "rgba(255,255,255,.6)", fontWeight: 300 }}>Consultorio Digital</div>
            </div>
          </div>
        </div>

        <div style={{ padding: "20px 16px", maxWidth: 640, margin: "0 auto", paddingBottom: "max(20px, env(safe-area-inset-bottom))" }}>
          {/* stats */}
          <div style={{ display: "grid", gridTemplateColumns: "repeat(3,1fr)", gap: 10, marginBottom: 20 }}>
            {[["Pacientes", patients.length], ["Hoy", todayCount], ["Este mes", monthCount]].map(([label, num]) => (
              <div key={label} style={{ background: "white", borderRadius: 14, padding: "16px 12px", textAlign: "center", boxShadow: "0 2px 12px rgba(13,92,99,.08)" }}>
                <div style={{ fontSize: 28, fontWeight: 800, color: TEAL }}>{num}</div>
                <div style={{ fontSize: 11, color: GRAY_400, marginTop: 2 }}>{label}</div>
              </div>
            ))}
          </div>

          {/* new button */}
          <button
            onClick={startNew}
            style={{ width: "100%", background: TEAL, color: "white", border: "none", borderRadius: 14, padding: "18px 20px", fontSize: 17, fontWeight: 700, cursor: "pointer", display: "flex", alignItems: "center", justifyContent: "center", gap: 10, boxShadow: "0 4px 16px rgba(13,92,99,.3)", marginBottom: 24, fontFamily: "inherit" }}
          >
            <span style={{ fontSize: 22 }}>＋</span> Nueva Historia Clínica
          </button>

          <div style={{ fontSize: 18, fontWeight: 700, color: GRAY_800, marginBottom: 4 }}>Historias guardadas</div>
          <div style={{ fontSize: 13, color: GRAY_400, marginBottom: 14 }}>
            {patients.length === 0 ? "Sin registros aún" : `${patients.length} historia${patients.length !== 1 ? "s" : ""} guardada${patients.length !== 1 ? "s" : ""}`}
          </div>

          {patients.length === 0 ? (
            <div style={{ background: "white", borderRadius: 14, padding: "48px 24px", textAlign: "center", boxShadow: "0 2px 12px rgba(13,92,99,.08)" }}>
              <div style={{ fontSize: 48, marginBottom: 12 }}>📋</div>
              <div style={{ fontSize: 18, fontWeight: 700, color: GRAY_600 }}>Sin pacientes aún</div>
              <div style={{ fontSize: 14, color: GRAY_400, marginTop: 6 }}>Toca "Nueva Historia Clínica" para comenzar</div>
            </div>
          ) : (
            <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
              {patients.map(p => (
                <div
                  key={p.id}
                  onClick={() => { setDetailId(p.id); setScreen("detail"); }}
                  style={{ background: "white", borderRadius: 14, padding: "16px 18px", display: "flex", alignItems: "center", justifyContent: "space-between", cursor: "pointer", boxShadow: "0 2px 12px rgba(13,92,99,.08)", borderLeft: `4px solid ${TEAL}` }}
                >
                  <div>
                    <div style={{ fontSize: 17, fontWeight: 700, color: GRAY_800 }}>{patientName(p)}</div>
                    <div style={{ fontSize: 12, color: GRAY_400, marginTop: 4 }}>
                      {new Date(p.savedAt).toLocaleDateString("es-MX", { day: "2-digit", month: "short", year: "numeric" })}
                      {p.edad ? ` · ${p.edad} años` : ""}
                      {p.sexo ? ` · ${p.sexo}` : ""}
                    </div>
                  </div>
                  <div style={{ background: TEAL_PALE, color: TEAL, fontSize: 12, fontWeight: 700, padding: "5px 12px", borderRadius: 50 }}>Ver</div>
                </div>
              ))}
            </div>
          )}
        </div>

        {toast && (
          <div style={{ position: "fixed", bottom: 24, left: "50%", transform: "translateX(-50%)", background: toast.type === "success" ? SUCCESS : GRAY_800, color: "white", padding: "13px 24px", borderRadius: 50, fontSize: 15, fontWeight: 500, whiteSpace: "nowrap", boxShadow: "0 4px 20px rgba(0,0,0,.2)", zIndex: 999 }}>
            {toast.msg}
          </div>
        )}
      </div>
    );
  }

  // ── FORM SCREEN ──
  if (screen === "form") {
    const total = SECTIONS.length;
    const pct = ((currentIdx + 1) / total * 100).toFixed(0);
    const SectionComp = SECTION_COMPONENTS[currentIdx];
    const isLast = currentIdx === total - 1;

    return (
      <div style={{ minHeight: "100vh", background: GRAY_100, fontFamily: "system-ui, -apple-system, sans-serif", display: "flex", flexDirection: "column" }}>
        {/* header */}
        <div style={{ background: TEAL, padding: "14px 16px", display: "flex", alignItems: "center", justifyContent: "space-between", position: "sticky", top: 0, zIndex: 10, paddingTop: "max(14px, env(safe-area-inset-top))" }}>
          <button onClick={() => setScreen("list")} style={{ background: "rgba(255,255,255,.15)", border: "1px solid rgba(255,255,255,.25)", color: "white", padding: "8px 16px", borderRadius: 50, fontSize: 14, fontWeight: 600, cursor: "pointer", fontFamily: "inherit" }}>
            ← Pacientes
          </button>
          <div style={{ fontSize: 13, color: "rgba(255,255,255,.8)", fontWeight: 500 }}>{SECTIONS[currentIdx].icon} {SECTIONS[currentIdx].name}</div>
          <div style={{ fontSize: 13, color: "rgba(255,255,255,.6)" }}>{currentIdx + 1}/{total}</div>
        </div>

        {/* progress */}
        <div style={{ background: "white", padding: "10px 16px", borderBottom: `1px solid ${GRAY_200}` }}>
          <div style={{ height: 4, background: GRAY_200, borderRadius: 99, overflow: "hidden" }}>
            <div style={{ height: "100%", width: pct + "%", background: `linear-gradient(90deg, ${TEAL}, ${TEAL_LIGHT})`, borderRadius: 99, transition: "width .4s cubic-bezier(.4,0,.2,1)" }} />
          </div>
          <div style={{ display: "flex", gap: 5, marginTop: 8, justifyContent: "center" }}>
            {SECTIONS.map((_, i) => (
              <div key={i} style={{ width: 7, height: 7, borderRadius: "50%", background: i < currentIdx ? TEAL_LIGHT : i === currentIdx ? TEAL : GRAY_200, transform: i === currentIdx ? "scale(1.4)" : "scale(1)", transition: "all .2s", flexShrink: 0 }} />
            ))}
          </div>
        </div>

        {/* content */}
        <div style={{ flex: 1, overflowY: "auto", padding: "24px 16px", maxWidth: 640, width: "100%", margin: "0 auto", boxSizing: "border-box" }}>
          <SectionComp f={form} set={setField} />
        </div>

        {/* nav */}
        <div style={{ background: "white", borderTop: `1px solid ${GRAY_200}`, padding: "14px 16px", display: "flex", gap: 12, maxWidth: 640, width: "100%", margin: "0 auto", boxSizing: "border-box", paddingBottom: "max(14px, env(safe-area-inset-bottom))" }}>
          {currentIdx > 0 && (
            <button
              onClick={() => setCurrentIdx(i => i - 1)}
              style={{ padding: "15px 20px", border: `2px solid ${GRAY_200}`, borderRadius: 12, background: "white", fontSize: 16, fontWeight: 600, cursor: "pointer", color: GRAY_600, fontFamily: "inherit" }}
            >‹ Atrás</button>
          )}
          {isLast ? (
            <button
              onClick={savePatient}
              style={{ flex: 1, padding: "15px 20px", border: "none", borderRadius: 12, background: GOLD, color: "white", fontSize: 16, fontWeight: 700, cursor: "pointer", fontFamily: "inherit", boxShadow: `0 4px 14px rgba(201,150,58,.35)` }}
            >💾 Guardar Historia</button>
          ) : (
            <button
              onClick={() => setCurrentIdx(i => i + 1)}
              style={{ flex: 1, padding: "15px 20px", border: "none", borderRadius: 12, background: TEAL, color: "white", fontSize: 16, fontWeight: 700, cursor: "pointer", fontFamily: "inherit", boxShadow: `0 4px 14px rgba(13,92,99,.28)` }}
            >Siguiente ›</button>
          )}
        </div>

        {toast && (
          <div style={{ position: "fixed", bottom: 24, left: "50%", transform: "translateX(-50%)", background: toast.type === "success" ? SUCCESS : GRAY_800, color: "white", padding: "13px 24px", borderRadius: 50, fontSize: 15, fontWeight: 500, whiteSpace: "nowrap", boxShadow: "0 4px 20px rgba(0,0,0,.2)", zIndex: 999 }}>
            {toast.msg}
          </div>
        )}
      </div>
    );
  }

  // ── DETAIL SCREEN ──
  if (screen === "detail") {
    const p = patients.find(x => x.id === detailId);
    if (!p) { setScreen("list"); return null; }
    const name = patientName(p);

    const Row = ({ label, value }) => value ? (
      <div style={{ display: "flex", gap: 8, marginBottom: 8, flexWrap: "wrap" }}>
        <span style={{ fontSize: 13, color: GRAY_400, fontWeight: 500, minWidth: 130 }}>{label}</span>
        <span style={{ fontSize: 13, color: GRAY_800, flex: 1 }}>{Array.isArray(value) ? value.join(", ") : value}</span>
      </div>
    ) : null;

    const Section = ({ title, children }) => (
      <div style={{ marginBottom: 20, paddingBottom: 20, borderBottom: `1px solid ${GRAY_200}` }}>
        <div style={{ fontSize: 11, fontWeight: 700, textTransform: "uppercase", letterSpacing: ".8px", color: TEAL, marginBottom: 10 }}>{title}</div>
        {children}
      </div>
    );

    return (
      <div style={{ minHeight: "100vh", background: GRAY_100, fontFamily: "system-ui, -apple-system, sans-serif" }}>
        <div style={{ background: TEAL, padding: "14px 16px", display: "flex", alignItems: "center", justifyContent: "space-between", position: "sticky", top: 0, zIndex: 10, paddingTop: "max(14px, env(safe-area-inset-top))" }}>
          <button onClick={() => setScreen("list")} style={{ background: "rgba(255,255,255,.15)", border: "1px solid rgba(255,255,255,.25)", color: "white", padding: "8px 16px", borderRadius: 50, fontSize: 14, fontWeight: 600, cursor: "pointer", fontFamily: "inherit" }}>
            ← Pacientes
          </button>
          <div style={{ fontSize: 14, color: "rgba(255,255,255,.9)", fontWeight: 600 }}>Expediente</div>
          <div style={{ width: 70 }} />
        </div>

        <div style={{ padding: "20px 16px", maxWidth: 640, margin: "0 auto", paddingBottom: "max(20px, env(safe-area-inset-bottom))" }}>
          <div style={{ background: "white", borderRadius: 14, padding: "20px 18px", boxShadow: "0 2px 12px rgba(13,92,99,.08)", marginBottom: 16 }}>
            <div style={{ fontSize: 26, fontWeight: 800, color: TEAL, marginBottom: 4 }}>{name}</div>
            <div style={{ fontSize: 13, color: GRAY_400 }}>Guardado: {new Date(p.savedAt).toLocaleString("es-MX")}</div>
          </div>

          <div style={{ background: "white", borderRadius: 14, padding: "20px 18px", boxShadow: "0 2px 12px rgba(13,92,99,.08)" }}>
            <Section title="📋 Control">
              <Row label="Folio" value={p.folio} /><Row label="Fecha" value={p.fecha} /><Row label="Hora" value={p.hora} />
            </Section>
            <Section title="👤 Datos Generales">
              <Row label="Edad" value={p.edad ? p.edad + " años" : null} />
              <Row label="Sexo" value={p.sexo} /><Row label="Estado civil" value={p.estadoCivil} />
              <Row label="Teléfono" value={p.telMovil || p.telPart} /><Row label="Ocupación" value={p.ocupacion} />
            </Section>
            <Section title="👨‍👩‍👧 Heredo-familiares">
              <Row label="Padre" value={p.padre_estado ? `${p.padre_estado} — ${p.padre_enf || ""}` : null} />
              <Row label="Madre" value={p.madre_estado ? `${p.madre_estado} — ${p.madre_enf || ""}` : null} />
            </Section>
            <Section title="🏥 Antecedentes Patológicos">
              <Row label="Al. quirúrgicas" value={p.alQuir} /><Row label="Al. médicas" value={p.alMed} />
              <Row label="Diabetes" value={p.diabetes} /><Row label="Hipertensión" value={p.hipertension} />
              <Row label="Cardiacos" value={p.cardiacos} /><Row label="Vasculares" value={p.vasculares} />
            </Section>
            <Section title="🍃 No Patológicos">
              <Row label="Tabaquismo" value={p.tabaquismo} /><Row label="Alcohol" value={p.alcohol} /><Row label="Vacunas" value={p.vacunas} />
            </Section>
            <Section title="🔍 Exploración Física">
              <Row label="Marcha" value={p.marcha} /><Row label="Traslados" value={p.traslados} />
            </Section>
            <Section title="📊 Escala de Dolor">
              <Row label="Nivel" value={p.dolor !== undefined ? `${p.dolor}/10 — ${PAIN_LABELS[p.dolor]}` : null} />
            </Section>
            <Section title="💊 Tratamiento Actual">
              <Row label="Tratamiento" value={p.tratActual} />
            </Section>
            <Section title="🩺 Diagnóstico">
              <Row label="Diagnóstico" value={p.diagnostico} />
            </Section>
            <Section title="📝 Plan de Tratamiento">
              <Row label="Objetivos" value={p.planObj} /><Row label="Prioridades" value={p.planPrio} /><Row label="Métodos" value={p.planMetodos} />
            </Section>
            <Section title="💬 Observaciones">
              <Row label="Notas" value={p.observaciones} />
            </Section>
            <Section title="✅ Validación">
              <Row label="Profesional" value={p.profesional} /><Row label="Cédula" value={p.cedula} /><Row label="Fecha cierre" value={p.fechaCierre} />
            </Section>

            <button
              onClick={() => deletePatient(p.id)}
              style={{ width: "100%", padding: 15, border: "none", borderRadius: 12, background: DANGER_LIGHT, color: DANGER, fontSize: 15, fontWeight: 700, cursor: "pointer", fontFamily: "inherit", marginTop: 8 }}
            >🗑 Eliminar registro</button>
          </div>
        </div>

        {toast && (
          <div style={{ position: "fixed", bottom: 24, left: "50%", transform: "translateX(-50%)", background: toast.type === "success" ? SUCCESS : GRAY_800, color: "white", padding: "13px 24px", borderRadius: 50, fontSize: 15, fontWeight: 500, whiteSpace: "nowrap", boxShadow: "0 4px 20px rgba(0,0,0,.2)", zIndex: 999 }}>
            {toast.msg}
          </div>
        )}
      </div>
    );
  }
}
