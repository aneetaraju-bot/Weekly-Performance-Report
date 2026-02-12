import { useState } from "react";
import { BarChart, Bar, XAxis, YAxis, Tooltip, ResponsiveContainer, Cell } from "recharts";

const data = {
  "Coding": {
    color: "#f97316",
    icon: "💻",
    categories: [
      { name: "Coding ML",  bh: 22.64, prevBh: 23.09, ap: 73.21, prevAp: 73.72, lct: 43.49, prevLct: 43.90, rating: 4.52 },
      { name: "Coding TE",  bh: 15.45, prevBh: 8.97,  ap: 65.59, prevAp: 60.31, lct: 36.42, prevLct: 24.00, rating: 4.67 },
      { name: "Coding TN",  bh: 15.95, prevBh: 15.05, ap: 68.94, prevAp: 67.69, lct: 29.74, prevLct: 27.33, rating: 4.67 },
    ]
  },
  "Commerce": {
    color: "#eab308",
    icon: "🏦",
    categories: [
      { name: "Commerce ML", bh: 33.07, prevBh: 32.87, ap: 73.14, prevAp: 73.09, lct: 48.71, prevLct: 46.64, rating: 4.63 },
      { name: "Commerce TN", bh: 35.63, prevBh: 35.72, ap: 74.50, prevAp: 77.08, lct: 75.50, prevLct: 76.15, rating: 4.63 },
    ]
  },
  "Digital Marketing": {
    color: "#10b981",
    icon: "📣",
    categories: [
      { name: "Dig Mktg ML", bh: 31.82, prevBh: 28.19, ap: 73.99, prevAp: 71.55, lct: 46.82, prevLct: 44.28, rating: 4.59 },
      { name: "Dig Mktg TN", bh: 29.16, prevBh: 30.57, ap: 74.01, prevAp: 75.35, lct: 48.66, prevLct: 48.56, rating: 4.59 },
    ]
  },
  "Healthcare": {
    color: "#06b6d4",
    icon: "🏥",
    categories: [
      { name: "Hospital ML", bh: 45.96, prevBh: 46.77, ap: 78.97, prevAp: 79.27, lct: 57.59, prevLct: 57.56, rating: 4.73 },
    ]
  },
  "Teaching": {
    color: "#ec4899",
    icon: "🎓",
    categories: [
      { name: "Teaching ML", bh: 34.40, prevBh: 34.90, ap: 68.84, prevAp: 69.36, lct: 38.27, prevLct: 37.53, rating: 4.83 },
      { name: "Teaching TN", bh: 50.54, prevBh: 52.06, ap: 86.41, prevAp: 87.39, lct: 98.47, prevLct: 98.40, rating: 4.83 },
    ]
  },
  "Technical": {
    color: "#8b5cf6",
    icon: "🔧",
    categories: [
      { name: "Technical ML", bh: 35.36, prevBh: 34.64, ap: 77.42, prevAp: 77.38, lct: 42.47, prevLct: 42.68, rating: 4.52 },
      { name: "Technical TE", bh: 36.93, prevBh: 36.36, ap: 74.96, prevAp: 74.10, lct: 43.71, prevLct: 44.38, rating: 4.52 },
      { name: "Technical TN", bh: 38.47, prevBh: 38.06, ap: 76.82, prevAp: 76.81, lct: 43.53, prevLct: 43.69, rating: 4.52 },
    ]
  }
};

const METRICS = [
  { key: "bh",     label: "Batch Health",        unit: "%",  max: 60,  prevKey: "prevBh",  warn: 20, ok: 35 },
  { key: "ap",     label: "Active Participation", unit: "%",  max: 100, prevKey: "prevAp",  warn: 65, ok: 75 },
  { key: "lct",    label: "LCT On-Time",          unit: "%",  max: 100, prevKey: "prevLct", warn: 40, ok: 60 },
  { key: "rating", label: "Live Rating",          unit: "★",  max: 5,   prevKey: null,      warn: 4.2, ok: 4.5 },
];

const getColor = (val, warn, ok) => {
  if (val >= ok)   return { text: "#16a34a", bg: "#f0fdf4" };
  if (val >= warn) return { text: "#d97706", bg: "#fffbeb" };
  return               { text: "#dc2626", bg: "#fef2f2" };
};

const Delta = ({ curr, prev }) => {
  if (prev == null) return null;
  const d = (curr - prev).toFixed(2);
  const up = d >= 0;
  return (
    <span style={{ fontSize: 10, color: up ? "#16a34a" : "#dc2626", fontWeight: 700 }}>
      {up ? " ▲" : " ▼"}{Math.abs(d)}
    </span>
  );
};

const MiniBar = ({ value, max, warn, ok }) => {
  const pct = Math.min((value / max) * 100, 100);
  const { text: barColor } = getColor(value, warn, ok);
  return (
    <div style={{ height: 5, background: "#f1f5f9", borderRadius: 3, width: "100%", marginTop: 5 }}>
      <div style={{ width: `${pct}%`, height: "100%", background: barColor, borderRadius: 3 }} />
    </div>
  );
};

const MetricCell = ({ value, prev, unit, warn, ok, max }) => {
  const { text, bg } = getColor(value, warn, ok);
  return (
    <td style={{ padding: "12px 14px", textAlign: "center", verticalAlign: "middle" }}>
      <div style={{ display: "inline-flex", flexDirection: "column", alignItems: "center", minWidth: 90 }}>
        <div style={{ background: bg, borderRadius: 8, padding: "4px 10px", marginBottom: 4 }}>
          <span style={{ fontSize: 15, fontWeight: 700, color: text, fontFamily: "'Figtree', sans-serif" }}>
            {value}{unit}
          </span>
          <Delta curr={value} prev={prev} />
        </div>
        <MiniBar value={value} max={max} warn={warn} ok={ok} />
        {prev != null && (
          <span style={{ fontSize: 9, color: "#a1a1aa", marginTop: 3, fontFamily: "'Figtree', sans-serif" }}>
            prev {prev}{unit}
          </span>
        )}
      </div>
    </td>
  );
};

export default function VerticalReport() {
  const [selected, setSelected] = useState("All");
  const verticals = Object.keys(data);
  const filtered = selected === "All" ? verticals : [selected];

  const allCats = verticals.flatMap(vn =>
    data[vn].categories.map(c => ({ ...c, vColor: data[vn].color }))
  );

  return (
    <div style={{ minHeight: "100vh", background: "#f4f4f5", fontFamily: "'Figtree', sans-serif" }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Figtree:wght@300;400;500;600;700&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; }
        @keyframes rise { from{opacity:0;transform:translateY(12px)} to{opacity:1;transform:translateY(0)} }
        .rise { animation: rise 0.4s ease both; }
        .filt:hover { background: #e4e4e7 !important; }
        tr.catrow:hover td { background: #fafaf8 !important; }
        @media print { .no-print{display:none!important} body{background:#fff!important} }
      `}</style>

      {/* HEADER */}
      <div style={{ background: "#18181b", padding: "20px 32px", display: "flex", justifyContent: "space-between", alignItems: "center", flexWrap: "wrap", gap: 12 }}>
        <div>
          <div style={{ fontSize: 9, letterSpacing: 3, color: "#52525b", textTransform: "uppercase", marginBottom: 4 }}>Entri · Weekly Report</div>
          <h1 style={{ fontFamily: "'Instrument Serif', serif", fontSize: "clamp(20px,3vw,30px)", color: "#fafafa", fontStyle: "italic", lineHeight: 1.1 }}>
            Vertical &amp; Category <span style={{ color: "#facc15", fontStyle: "normal" }}>Performance</span>
          </h1>
          <div style={{ fontSize: 10, color: "#52525b", marginTop: 3 }}>Feb 02 vs Feb 09, 2026</div>
        </div>
        <div style={{ display: "flex", gap: 10, alignItems: "center" }}>
          {[
            ["32.02%","Batch Health","#f97316"],
            ["73.20%","Active Partic.","#10b981"],
            ["47.72%","LCT On-Time","#06b6d4"],
            ["4.66★","Live Rating","#facc15"],
          ].map(([v, l, c]) => (
            <div key={l} style={{ background: "#27272a", borderRadius: 10, padding: "8px 14px", textAlign: "center", borderTop: `2px solid ${c}` }}>
              <div style={{ fontFamily: "'Instrument Serif', serif", fontSize: 17, color: "#fafafa", fontWeight: 700, lineHeight: 1 }}>{v}</div>
              <div style={{ fontSize: 9, color: "#71717a", marginTop: 3, letterSpacing: 0.4 }}>{l}</div>
              <div style={{ fontSize: 8, color: "#52525b", marginTop: 1 }}>Grand Total</div>
            </div>
          ))}
          <button onClick={() => window.print()} className="no-print" style={{ background: "#facc15", border: "none", borderRadius: 8, color: "#18181b", padding: "10px 16px", fontSize: 11, cursor: "pointer", fontWeight: 700 }}>↓ PDF</button>
        </div>
      </div>

      {/* FILTER */}
      <div style={{ background: "#fff", borderBottom: "1px solid #e4e4e7", padding: "10px 32px", display: "flex", gap: 6, flexWrap: "wrap", alignItems: "center" }} className="no-print">
        <span style={{ fontSize: 10, color: "#a1a1aa", marginRight: 4, letterSpacing: 0.5 }}>FILTER:</span>
        {["All", ...verticals].map(v => (
          <button key={v} className="filt" onClick={() => setSelected(v)} style={{
            background: selected === v ? "#18181b" : "#f4f4f5",
            color: selected === v ? "#fff" : "#52525b",
            border: "none", borderRadius: 20, padding: "5px 14px",
            fontSize: 11, cursor: "pointer", fontWeight: selected === v ? 600 : 400,
            display: "flex", alignItems: "center", gap: 4, fontFamily: "'Figtree', sans-serif",
          }}>
            {v !== "All" && data[v]?.icon} {v}
          </button>
        ))}
      </div>

      <div style={{ maxWidth: 1100, margin: "0 auto", padding: "24px 18px" }}>

        {/* COLOR LEGEND for metrics */}
        <div style={{ display: "flex", gap: 16, marginBottom: 20, alignItems: "center", flexWrap: "wrap" }}>
          <span style={{ fontSize: 10, color: "#71717a", letterSpacing: 0.5, textTransform: "uppercase" }}>Score guide:</span>
          {[["#16a34a","#f0fdf4","Good"],["#d97706","#fffbeb","Needs Attention"],["#dc2626","#fef2f2","Critical"]].map(([c,bg,lbl]) => (
            <div key={lbl} style={{ display: "flex", alignItems: "center", gap: 5, background: bg, borderRadius: 20, padding: "3px 12px", border: `1px solid ${c}33` }}>
              <div style={{ width: 7, height: 7, borderRadius: "50%", background: c }} />
              <span style={{ fontSize: 10, color: c, fontWeight: 600 }}>{lbl}</span>
            </div>
          ))}
        </div>

        {/* VERTICAL BLOCKS */}
        {filtered.map((vName, vi) => {
          const v = data[vName];
          // Compute vertical totals (sum of category values for display)
          const cats = v.categories;
          const totBh  = (cats.reduce((a, c) => a + c.bh,     0) / cats.length).toFixed(1);
          const totAp  = (cats.reduce((a, c) => a + c.ap,     0) / cats.length).toFixed(1);
          const totLct = (cats.reduce((a, c) => a + c.lct,    0) / cats.length).toFixed(1);
          const totRt  = (cats.reduce((a, c) => a + c.rating, 0) / cats.length).toFixed(2);

          return (
            <div key={vName} className="rise" style={{ animationDelay: `${vi * 0.06}s`, marginBottom: 18, background: "#fff", borderRadius: 14, boxShadow: "0 1px 6px rgba(0,0,0,0.06)", border: "1px solid #e4e4e7", overflow: "hidden" }}>

              {/* Vertical Header Row */}
              <div style={{ background: `linear-gradient(90deg, ${v.color}22 0%, #fff 100%)`, padding: "13px 22px", borderBottom: `1.5px solid ${v.color}44`, display: "flex", justifyContent: "space-between", alignItems: "center", flexWrap: "wrap", gap: 10 }}>
                <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                  <div style={{ width: 36, height: 36, borderRadius: 10, background: `${v.color}20`, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 18 }}>{v.icon}</div>
                  <div>
                    <h2 style={{ fontFamily: "'Instrument Serif', serif", fontSize: 19, color: "#18181b", fontStyle: "italic", lineHeight: 1 }}>{vName}</h2>
                    <div style={{ fontSize: 10, color: "#a1a1aa", marginTop: 2 }}>{cats.length} categor{cats.length > 1 ? "ies" : "y"} · values below are per-category actuals</div>
                  </div>
                </div>
                {/* Vertical-level summary — clearly labelled as vertical total */}
                <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
                  {[
                    ["Batch Health",totBh,"%",20,35],
                    ["Active Partic.",totAp,"%",65,75],
                    ["LCT On-Time",totLct,"%",40,60],
                    ["Live Rating",totRt,"★",4.2,4.5],
                  ].map(([lbl, val, unit, warn, ok]) => {
                    const { text, bg } = getColor(parseFloat(val), warn, ok);
                    return (
                      <div key={lbl} style={{ background: bg, border: `1px solid ${text}33`, borderRadius: 8, padding: "5px 12px", textAlign: "center" }}>
                        <div style={{ fontSize: 14, fontWeight: 700, color: text }}>{val}{unit}</div>
                        <div style={{ fontSize: 9, color: "#71717a", marginTop: 1 }}>{lbl}</div>
                        <div style={{ fontSize: 8, color: "#a1a1aa" }}>vertical avg</div>
                      </div>
                    );
                  })}
                </div>
              </div>

              {/* Category Table */}
              <div style={{ overflowX: "auto" }}>
                <table style={{ width: "100%", borderCollapse: "collapse" }}>
                  <thead>
                    <tr style={{ background: "#fafaf8", borderBottom: "1px solid #e4e4e7" }}>
                      <th style={{ padding: "9px 22px", textAlign: "left", fontSize: 10, color: "#a1a1aa", letterSpacing: 0.8, textTransform: "uppercase", fontWeight: 600 }}>Category</th>
                      {METRICS.map(m => (
                        <th key={m.key} style={{ padding: "9px 14px", textAlign: "center", fontSize: 10, color: "#a1a1aa", letterSpacing: 0.8, textTransform: "uppercase", fontWeight: 600 }}>
                          {m.label}
                        </th>
                      ))}
                      <th style={{ padding: "9px 14px", textAlign: "center", fontSize: 10, color: "#a1a1aa", letterSpacing: 0.8, textTransform: "uppercase", fontWeight: 600 }}>Week Trend</th>
                    </tr>
                  </thead>
                  <tbody>
                    {cats.map((cat, ci) => {
                      const overallDelta = (cat.bh - cat.prevBh) + (cat.ap - cat.prevAp) + (cat.lct - cat.prevLct);
                      const trendUp = overallDelta >= 0;
                      return (
                        <tr key={cat.name} className="catrow" style={{ borderBottom: "1px solid #f4f4f5", background: ci % 2 === 0 ? "#fff" : "#fafaf8" }}>
                          {/* Name */}
                          <td style={{ padding: "12px 22px", verticalAlign: "middle" }}>
                            <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
                              <div style={{ width: 10, height: 10, borderRadius: 3, background: v.color, flexShrink: 0 }} />
                              <span style={{ fontWeight: 600, fontSize: 13, color: "#18181b" }}>{cat.name}</span>
                            </div>
                          </td>

                          {/* Batch Health */}
                          <MetricCell value={cat.bh}     prev={cat.prevBh}  unit="%" warn={20}  ok={35}  max={60} />
                          {/* Active Participation */}
                          <MetricCell value={cat.ap}     prev={cat.prevAp}  unit="%" warn={65}  ok={75}  max={100} />
                          {/* LCT */}
                          <MetricCell value={cat.lct}    prev={cat.prevLct} unit="%" warn={40}  ok={60}  max={100} />
                          {/* Rating */}
                          <MetricCell value={cat.rating} prev={null}        unit="★" warn={4.2} ok={4.5} max={5} />

                          {/* Trend */}
                          <td style={{ padding: "12px 14px", textAlign: "center", verticalAlign: "middle" }}>
                            <div style={{
                              display: "inline-flex", alignItems: "center", gap: 4,
                              background: trendUp ? "#f0fdf4" : "#fef2f2",
                              color: trendUp ? "#16a34a" : "#dc2626",
                              borderRadius: 20, padding: "5px 14px", fontSize: 11, fontWeight: 700,
                            }}>
                              {trendUp ? "▲" : "▼"} {trendUp ? "Improving" : "Declining"}
                            </div>
                          </td>
                        </tr>
                      );
                    })}
                  </tbody>
                </table>
              </div>
            </div>
          );
        })}

        {/* BOTTOM CHART — LCT All Categories */}
        {selected === "All" && (
          <div style={{ background: "#fff", borderRadius: 14, padding: "22px", marginTop: 8, border: "1px solid #e4e4e7", boxShadow: "0 1px 6px rgba(0,0,0,0.05)" }}>
            <h3 style={{ fontFamily: "'Instrument Serif', serif", fontSize: 18, color: "#18181b", fontStyle: "italic", marginBottom: 2 }}>LCT On-Time Completion — All Categories</h3>
            <p style={{ fontSize: 11, color: "#a1a1aa", marginBottom: 18 }}>This week vs last week · per category</p>
            <ResponsiveContainer width="100%" height={200}>
              <BarChart
                data={verticals.flatMap(vn => data[vn].categories.map(c => ({ name: c.name, thisWeek: c.lct, lastWeek: c.prevLct, color: data[vn].color })))}
                margin={{ top: 4, right: 8, bottom: 48, left: -10 }}
              >
                <XAxis dataKey="name" tick={{ fontSize: 9, fill: "#a1a1aa" }} axisLine={false} tickLine={false} angle={-38} textAnchor="end" interval={0} />
                <YAxis tick={{ fontSize: 9, fill: "#a1a1aa" }} axisLine={false} tickLine={false} unit="%" domain={[0, 105]} />
                <Tooltip contentStyle={{ background: "#18181b", border: "none", borderRadius: 8, fontSize: 11, color: "#fafafa" }} formatter={(v) => [`${v}%`]} />
                <Bar dataKey="thisWeek" name="This Week" radius={[4,4,0,0]}>
                  {verticals.flatMap((vn, vi) => data[vn].categories.map((_, ci) => <Cell key={`${vi}-${ci}`} fill={data[vn].color} />))}
                </Bar>
                <Bar dataKey="lastWeek" name="Last Week" fill="#e4e4e7" radius={[4,4,0,0]} />
              </BarChart>
            </ResponsiveContainer>
          </div>
        )}

        <div style={{ textAlign: "center", marginTop: 24, fontSize: 9, color: "#d4d4d8", letterSpacing: 2, textTransform: "uppercase" }}>
          Entri · Weekly Performance Report · Feb 09, 2026
        </div>
      </div>
    </div>
  );
}
