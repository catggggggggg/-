<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>モンストガイドマスター</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <style>
    body { overscroll-behavior: none; -webkit-touch-callout: none; -webkit-user-select: none; user-select: none; }
    .pb-safe { padding-bottom: env(safe-area-inset-bottom, 20px); }
  </style>
</head>
<body class="bg-slate-950">
  <div id="root"></div>
  <script type="text/babel">
    const { useState, useRef, useEffect, useCallback } = React;

    // --- Icons ---
    const IconCrosshair = () => <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><circle cx="12" cy="12" r="10"/><line x1="22" y1="12" x2="18" y2="12"/><line x1="6" y1="12" x2="2" y2="12"/><line x1="12" y1="6" x2="12" y2="2"/><line x1="12" y1="22" x2="12" y2="18"/></svg>;
    const IconUpload = () => <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>;
    const IconHand = ({ size = 20 }) => <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M18 11V6a2 2 0 0 0-2-2v0a2 2 0 0 0-2 2v0"/><path d="M14 10V4a2 2 0 0 0-2-2v0a2 2 0 0 0-2 2v2"/><path d="M10 10.5V6a2 2 0 0 0-2-2v0a2 2 0 0 0-2 2v8"/><path d="M18 8a2 2 0 1 1 4 0v6a8 8 0 0 1-8 8h-2c-2.8 0-4.5-.86-5.99-2.34l-3.6-3.6a2 2 0 0 1 2.83-2.82L7 15"/><path d="M6 11V9a2 2 0 0 0-2-2v0a2 2 0 0 0-2 2v5"/></svg>;
    const IconRefresh = () => <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><polyline points="23 4 23 10 17 10"/><polyline points="1 20 1 14 7 14"/><path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"/></svg>;
    const IconTrash = () => <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path></svg>;
    const IconCheck = () => <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="3" strokeLinecap="round" strokeLinejoin="round"><polyline points="20 6 9 17 4 12"></polyline></svg>;
    const IconUndo = () => <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2.5" strokeLinecap="round" strokeLinejoin="round"><path d="M9 14L4 9l5-5" /><path d="M4 9h10.5a5.5 5.5 0 0 1 5.5 5.5v0a5.5 5.5 0 0 1-5.5 5.5H11" /></svg>;
    const IconRedo = () => <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2.5" strokeLinecap="round" strokeLinejoin="round"><path d="M15 14l5-5-5-5" /><path d="M20 9H9.5A5.5 5.5 0 0 0 4 14.5v0A5.5 5.5 0 0 0 9.5 20H13" /></svg>;
    const IconSave = () => <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg>;

    const App = () => {
      const [image, setImage] = useState(null);
      const [startPoint, setStartPoint] = useState({ x: 195, y: 550 });
      const [angle, setAngle] = useState(45);
      const [isMoveMode, setIsMoveMode] = useState(false);

      // App Settings
      const [maxBounces, setMaxBounces] = useState(3);
      const [showReverseGuide, setShowReverseGuide] = useState(true);
      const [showBand, setShowBand] = useState(false);
      const [showTrajectory, setShowTrajectory] = useState(true);
      const [showWallLine, setShowWallLine] = useState(true);
      const [lineColor, setLineColor] = useState('white');

      // Wall Settings
      const defaultWalls = { top: 19, bottom: 33, left: 5, right: 5 };
      const tabletWalls = { top: 12, bottom: 18, left: 12, right: 12 };
      const [wallPercents, setWallPercents] = useState(defaultWalls);

      // Obstacles & Warps
      const [obstacles, setObstacles] = useState([]);
      const [previewObs, setPreviewObs] = useState(null);
      const [obsMode, setObsMode] = useState('edit'); 
      const [selectedIds, setSelectedIds] = useState([]); 
      const [warps, setWarps] = useState([]);
      const [obsType, setObsType] = useState('block');

      const [activeTab, setActiveTab] = useState('aim'); 
      const [dragMode, setDragMode] = useState(null); 
      const obsDragRef = useRef(null);

      // Save States
      const [saveName, setSaveName] = useState('');
      const [savedStages, setSavedStages] = useState(() => {
        try { return JSON.parse(localStorage.getItem('monst_saved_stages') || '[]'); } catch (e) { return []; }
      });

      // Undo / Redo History
      const [history, setHistory] = useState([]);
      const [historyIndex, setHistoryIndex] = useState(-1);
      const isHistoryChange = useRef(false);

      const canvasRef = useRef(null);
      const fileInputRef = useRef(null);

      const canvasWidth = 390;
      const canvasHeight = 844;

      const bounds = {
        left: canvasWidth * (wallPercents.left / 100),
        right: canvasWidth * (1 - wallPercents.right / 100),
        top: canvasHeight * (wallPercents.top / 100),
        bottom: canvasHeight * (1 - wallPercents.bottom / 100),
      };

      const cropMargin = 20; 
      const viewBounds = {
        left: Math.max(0, bounds.left - cropMargin),
        right: Math.min(canvasWidth, bounds.right + cropMargin),
        top: Math.max(0, bounds.top - cropMargin),
        bottom: Math.min(canvasHeight, bounds.bottom + cropMargin),
      };
      const viewWidth = viewBounds.right - viewBounds.left;
      const viewHeight = viewBounds.bottom - viewBounds.top;

      // History Management
      const pushHistory = useCallback(() => {
        if (isHistoryChange.current) {
          isHistoryChange.current = false;
          return;
        }
        const state = { startPoint, angle, maxBounces, wallPercents, obstacles, warps };
        setHistory(prev => {
          const next = prev.slice(0, historyIndex + 1);
          return [...next, state];
        });
        setHistoryIndex(prev => prev + 1);
      }, [startPoint, angle, maxBounces, wallPercents, obstacles, warps, historyIndex]);

      useEffect(() => {
        if (history.length === 0) pushHistory();
      }, [pushHistory, history.length]);

      const pushHistoryDebounced = () => {
        setTimeout(pushHistory, 100);
      };

      const handleUndo = () => {
        if (historyIndex > 0) {
          isHistoryChange.current = true;
          const prev = history[historyIndex - 1];
          setStartPoint(prev.startPoint);
          setAngle(prev.angle);
          setMaxBounces(prev.maxBounces);
          setWallPercents(prev.wallPercents);
          setObstacles(prev.obstacles);
          setWarps(prev.warps);
          setHistoryIndex(historyIndex - 1);
        }
      };

      const handleRedo = () => {
        if (historyIndex < history.length - 1) {
          isHistoryChange.current = true;
          const next = history[historyIndex + 1];
          setStartPoint(next.startPoint);
          setAngle(next.angle);
          setMaxBounces(next.maxBounces);
          setWallPercents(next.wallPercents);
          setObstacles(next.obstacles);
          setWarps(next.warps);
          setHistoryIndex(historyIndex + 1);
        }
      };

      const handleSaveStage = () => {
        if (!saveName.trim()) return;
        const newStage = {
          id: Date.now(),
          name: saveName.trim(),
          obstacles,
          warps,
          wallPercents,
          date: new Date().toLocaleDateString('ja-JP')
        };
        const updated = [newStage, ...savedStages];
        setSavedStages(updated);
        localStorage.setItem('monst_saved_stages', JSON.stringify(updated));
        setSaveName('');
      };

      const handleLoadStage = (stage) => {
        setObstacles(stage.obstacles || []);
        setWarps(stage.warps || []);
        if (stage.wallPercents) setWallPercents(stage.wallPercents);
        setTimeout(pushHistory, 100);
      };

      const handleDeleteStage = (id) => {
        const updated = savedStages.filter(s => s.id !== id);
        setSavedStages(updated);
        localStorage.setItem('monst_saved_stages', JSON.stringify(updated));
      };

      const handleImageUpload = (e) => {
        const file = e.target.files?.[0];
        if (file) {
          const reader = new FileReader();
          reader.onload = (event) => {
            const img = new Image();
            img.onload = () => setImage(img);
            img.src = event.target.result;
          };
          reader.readAsDataURL(file);
        }
      };

      const getCanvasCoords = (clientX, clientY) => {
        const canvas = canvasRef.current;
        if (!canvas) return null;
        const rect = canvas.getBoundingClientRect();
        const scaleX = viewWidth / rect.width;
        const scaleY = viewHeight / rect.height;
        return {
          x: (clientX - rect.left) * scaleX + viewBounds.left,
          y: (clientY - rect.top) * scaleY + viewBounds.top
        };
      };

      // --- Interaction Start ---
      const startInteraction = (coords) => {
        if (!coords) return;

        if (activeTab === 'obstacles') {
          if (obsMode === 'delete') {
            const hitObs = obstacles.find(o => coords.x >= o.x && coords.x <= o.x + o.w && coords.y >= o.y && coords.y <= o.y + o.h);
            if (hitObs) {
              setSelectedIds(prev => prev.includes(hitObs.id) ? prev.filter(id => id !== hitObs.id) : [...prev, hitObs.id]);
              return;
            }
            const hitWarp = warps.find(w => Math.hypot(coords.x - w.in.x, coords.y - w.in.y) < 25 || Math.hypot(coords.x - w.out.x, coords.y - w.out.y) < 25);
            if (hitWarp) {
              setSelectedIds(prev => prev.includes(hitWarp.id) ? prev.filter(id => id !== hitWarp.id) : [...prev, hitWarp.id]);
              return;
            }
            return;
          }

          if (obsMode === 'edit') {
            if (previewObs) {
              const cornerSize = 24; 
              const corners = [
                { type: 'lt', x: previewObs.x, y: previewObs.y },
                { type: 'rt', x: previewObs.x + previewObs.w, y: previewObs.y },
                { type: 'lb', x: previewObs.x, y: previewObs.y + previewObs.h },
                { type: 'rb', x: previewObs.x + previewObs.w, y: previewObs.y + previewObs.h }
              ];
              for (const c of corners) {
                if (Math.abs(coords.x - c.x) < cornerSize && Math.abs(coords.y - c.y) < cornerSize) {
                   obsDragRef.current = { type: c.type, offsetX: c.x - coords.x, offsetY: c.y - coords.y };
                   return;
                }
              }
              if (coords.x >= previewObs.x && coords.x <= previewObs.x + previewObs.w && coords.y >= previewObs.y && coords.y <= previewObs.y + previewObs.h) {
                obsDragRef.current = { type: 'move', offsetX: previewObs.x - coords.x, offsetY: previewObs.y - coords.y };
                return;
              }
            } else {
              const size = 30;
              for (const warp of warps) {
                if (Math.hypot(coords.x - warp.in.x, coords.y - warp.in.y) < size) {
                  setDragMode('warp-in'); obsDragRef.current = { id: warp.id, offsetX: warp.in.x - coords.x, offsetY: warp.in.y - coords.y }; return;
                }
                if (Math.hypot(coords.x - warp.out.x, coords.y - warp.out.y) < size) {
                  setDragMode('warp-out'); obsDragRef.current = { id: warp.id, offsetX: warp.out.x - coords.x, offsetY: warp.out.y - coords.y }; return;
                }
              }

              for (let i = obstacles.length - 1; i >= 0; i--) {
                const o = obstacles[i];
                if (coords.x >= o.x && coords.x <= o.x + o.w && coords.y >= o.y && coords.y <= o.y + o.h) {
                  setPreviewObs({ ...o });
                  setObstacles(obstacles.filter(obs => obs.id !== o.id));
                  return;
                }
              }

              if (obsType === 'block') {
                const s = 60;
                setPreviewObs({ id: Date.now(), x: coords.x - s/2, y: coords.y - s/2, w: s, h: s });
              } else if (obsType === 'warp') {
                setWarps([...warps, { id: Date.now(), in: { x: coords.x - 40, y: coords.y }, out: { x: coords.x + 40, y: coords.y }, outAngle: null }]);
                pushHistoryDebounced();
              }
            }
            return;
          }
        }

        if (activeTab === 'aim' || activeTab === 'walls') {
          const dist = Math.hypot(coords.x - startPoint.x, coords.y - startPoint.y);
          if (dist < 60) {
            setDragMode('origin');
          } else {
            setDragMode('angle');
            updateAngleFromCoords(coords);
          }
        }
      };

      // --- Interaction Move ---
      const moveInteraction = (coords) => {
        if (!coords) return;
        
        if (activeTab === 'obstacles') {
          if (dragMode === 'warp-in' || dragMode === 'warp-out') {
            const { id, offsetX, offsetY } = obsDragRef.current;
            setWarps(prev => prev.map(w => {
              if (w.id === id) {
                const nx = coords.x + offsetX;
                const ny = coords.y + offsetY;
                return dragMode === 'warp-in' ? { ...w, in: { x: nx, y: ny } } : { ...w, out: { x: nx, y: ny } };
              }
              return w;
            }));
            return;
          }
        }

        if (previewObs && obsDragRef.current) {
          const { type, offsetX, offsetY } = obsDragRef.current;
          const targetX = coords.x + offsetX;
          const targetY = coords.y + offsetY;

          if (type === 'move') {
            setPreviewObs(prev => ({ ...prev, x: targetX, y: targetY }));
          } else {
            setPreviewObs(prev => {
              let nx = prev.x, ny = prev.y, nw = prev.w, nh = prev.h;

              if (type.includes('l')) { 
                const right = prev.x + prev.w;
                nx = targetX; 
                nw = right - nx; 
              }
              if (type.includes('r')) { 
                nw = targetX - prev.x; 
              }
              if (type.includes('t')) { 
                const bottom = prev.y + prev.h;
                ny = targetY; 
                nh = bottom - ny; 
              }
              if (type.includes('b')) { 
                nh = targetY - prev.y; 
              }

              if (nw < 20) { if (type.includes('l')) nx = prev.x + prev.w - 20; nw = 20; }
              if (nh < 20) { if (type.includes('t')) ny = prev.y + prev.h - 20; nh = 20; }
              return { ...prev, x: nx, y: ny, w: nw, h: nh };
            });
          }
        } else if (dragMode === 'origin') {
          const clampedX = Math.max(bounds.left, Math.min(coords.x, bounds.right));
          const clampedY = Math.max(bounds.top, Math.min(coords.y, bounds.bottom));
          setStartPoint({ x: clampedX, y: clampedY });
        } else if (dragMode === 'angle') {
          updateAngleFromCoords(coords);
        }
      };

      const handleEnd = () => {
        if (dragMode === 'origin' || dragMode === 'angle' || dragMode === 'warp-in' || dragMode === 'warp-out') {
          pushHistoryDebounced();
        }
        setDragMode(null);
        obsDragRef.current = null;
      };

      const updateAngleFromCoords = (coords) => {
        const dx = coords.x - startPoint.x;
        const dy = coords.y - startPoint.y;
        let newAngle = Math.atan2(dy, dx) * (180 / Math.PI);
        if (newAngle < 0) newAngle += 360;
        setAngle(newAngle);
      };

      const handleTouchStart = (e) => {
        if (isMoveMode) return;
        if (e.touches.length === 1) startInteraction(getCanvasCoords(e.touches[0].clientX, e.touches[0].clientY));
        else handleEnd();
      };
      const handleTouchMove = (e) => {
        if (isMoveMode) return;
        if (e.touches.length === 1 && (dragMode || obsDragRef.current)) moveInteraction(getCanvasCoords(e.touches[0].clientX, e.touches[0].clientY));
      };
      const handleMouseDown = (e) => { if (!isMoveMode) startInteraction(getCanvasCoords(e.clientX, e.clientY)); };
      const handleMouseMove = (e) => { if (!isMoveMode && (dragMode || obsDragRef.current)) moveInteraction(getCanvasCoords(e.clientX, e.clientY)); };

      useEffect(() => {
        const canvas = canvasRef.current;
        if (!canvas) return;
        const preventSingleTouch = (e) => {
          if (isMoveMode) return;
          if (e.touches.length === 1 && e.cancelable) e.preventDefault();
        };
        canvas.addEventListener('touchstart', preventSingleTouch, { passive: false });
        canvas.addEventListener('touchmove', preventSingleTouch, { passive: false });
        return () => {
          canvas.removeEventListener('touchstart', preventSingleTouch);
          canvas.removeEventListener('touchmove', preventSingleTouch);
        };
      }, [isMoveMode]);

      // --- Calculate Path (軌道計算) ---
      const calculatePath = useCallback(() => {
        if (!showTrajectory) return [];
        const path = [{ x: startPoint.x, y: startPoint.y, nx: 0, ny: 0, type: 'normal' }];
        let rad = angle * (Math.PI / 180);
        let vx = Math.cos(rad);
        let vy = Math.sin(rad);
        let currentX = startPoint.x;
        let currentY = startPoint.y;

        const usedWarpIds = new Set();
        const EPSILON = 0.5;

        for (let i = 0; i < maxBounces; i++) {
          if (currentX <= bounds.left + EPSILON && vx < 0) vx = -vx;
          if (currentX >= bounds.right - EPSILON && vx > 0) vx = -vx;
          if (currentY <= bounds.top + EPSILON && vy < 0) vy = -vy;
          if (currentY >= bounds.bottom - EPSILON && vy > 0) vy = -vy;

          let tMin = Infinity;
          let nextX = currentX;
          let nextY = currentY;
          let hitNormalX = 0;
          let hitNormalY = 0;
          let hitWarp = null;

          if (vx > 0) { let t = (bounds.right - currentX) / vx; if (t > 0.1 && t < tMin) { let y = currentY + t * vy; if (y >= bounds.top - 0.5 && y <= bounds.bottom + 0.5) { tMin = t; nextX = bounds.right; nextY = y; hitNormalX = -1; hitNormalY = 0; } } }
          if (vx < 0) { let t = (bounds.left - currentX) / vx; if (t > 0.1 && t < tMin) { let y = currentY + t * vy; if (y >= bounds.top - 0.5 && y <= bounds.bottom + 0.5) { tMin = t; nextX = bounds.left; nextY = y; hitNormalX = 1; hitNormalY = 0; } } }
          if (vy > 0) { let t = (bounds.bottom - currentY) / vy; if (t > 0.1 && t < tMin) { let x = currentX + t * vx; if (x >= bounds.left - 0.5 && x <= bounds.right + 0.5) { tMin = t; nextX = x; nextY = bounds.bottom; hitNormalX = 0; hitNormalY = -1; } } }
          if (vy < 0) { let t = (bounds.top - currentY) / vy; if (t > 0.1 && t < tMin) { let x = currentX + t * vx; if (x >= bounds.left - 0.5 && x <= bounds.right + 0.5) { tMin = t; nextX = x; nextY = bounds.top; hitNormalX = 0; hitNormalY = 1; } } }

          for (const obs of obstacles) {
            if (vx > 0) { let t = (obs.x - currentX) / vx; if (t > 0.1 && t < tMin) { let y = currentY + t * vy; if (y >= obs.y - 0.5 && y <= obs.y + obs.h + 0.5) { tMin = t; nextX = obs.x; nextY = y; hitNormalX = -1; hitNormalY = 0; } } }
            if (vx < 0) { let t = ((obs.x + obs.w) - currentX) / vx; if (t > 0.1 && t < tMin) { let y = currentY + t * vy; if (y >= obs.y - 0.5 && y <= obs.y + obs.h + 0.5) { tMin = t; nextX = obs.x + obs.w; nextY = y; hitNormalX = 1; hitNormalY = 0; } } }
            if (vy > 0) { let t = (obs.y - currentY) / vy; if (t > 0.1 && t < tMin) { let x = currentX + t * vx; if (x >= obs.x - 0.5 && x <= obs.x + obs.w + 0.5) { tMin = t; nextX = x; nextY = obs.y; hitNormalX = 0; hitNormalY = -1; } } }
            if (vy < 0) { let t = ((obs.y + obs.h) - currentY) / vy; if (t > 0.1 && t < tMin) { let x = currentX + t * vx; if (x >= obs.x - 0.5 && x <= obs.x + obs.w + 0.5) { tMin = t; nextX = x; nextY = obs.y + obs.h; hitNormalX = 0; hitNormalY = 1; } } }
          }

          const warpSize = 25;
          for (const w of warps) {
            if (usedWarpIds.has(w.id)) continue;
            const a = vx * vx + vy * vy;
            const b = 2 * (vx * (currentX - w.in.x) + vy * (currentY - w.in.y));
            const c = (currentX - w.in.x) * (currentX - w.in.x) + (currentY - w.in.y) * (currentY - w.in.y) - warpSize * warpSize;
            const discriminant = b * b - 4 * a * c;
            if (discriminant >= 0) {
              const t1 = (-b - Math.sqrt(discriminant)) / (2 * a);
              if (t1 > 0.1 && t1 < tMin) { tMin = t1; nextX = currentX + t1 * vx; nextY = currentY + t1 * vy; hitNormalX = 0; hitNormalY = 0; hitWarp = w; }
            }
          }

          if (tMin === Infinity) break;
          
          path.push({ x: nextX, y: nextY, nx: hitNormalX, ny: hitNormalY, type: hitWarp ? 'warpIn' : 'normal' });

          if (hitWarp) {
            usedWarpIds.add(hitWarp.id);
            path.push({ x: hitWarp.out.x, y: hitWarp.out.y, nx: 0, ny: 0, type: 'warpOut' });
            currentX = hitWarp.out.x;
            currentY = hitWarp.out.y;
            if (hitWarp.outAngle !== null) {
              const r = hitWarp.outAngle * (Math.PI / 180);
              vx = Math.cos(r); vy = Math.sin(r);
            }
          } else {
            if (hitNormalX !== 0) vx = -vx;
            if (hitNormalY !== 0) vy = -vy;
            currentX = nextX;
            currentY = nextY;
          }
        }
        return path;
      }, [startPoint, angle, wallPercents, maxBounces, canvasWidth, canvasHeight, obstacles, warps, showTrajectory]);

      // --- Render Canvas ---
      useEffect(() => {
        const canvas = canvasRef.current;
        if (!canvas) return;
        const ctx = canvas.getContext('2d');
        const dpr = window.devicePixelRatio || 1;
        canvas.width = viewWidth * dpr;
        canvas.height = viewHeight * dpr;
        ctx.scale(dpr, dpr);
        ctx.translate(-viewBounds.left, -viewBounds.top);
        ctx.clearRect(0, 0, canvasWidth, canvasHeight);

        // 背景画像
        if (image) {
          ctx.save();
          const imgAspect = image.width / image.height;
          const canvasAspect = canvasWidth / canvasHeight;
          let drawW = imgAspect > canvasAspect ? canvasWidth : canvasHeight * imgAspect;
          let drawH = imgAspect > canvasAspect ? canvasWidth / imgAspect : canvasHeight;
          ctx.translate(canvasWidth / 2, canvasHeight / 2);
          ctx.drawImage(image, -drawW / 2, -drawH / 2, drawW, drawH);
          ctx.restore();
        } else {
          ctx.fillStyle = '#0f172a';
          ctx.fillRect(0, 0, canvasWidth, canvasHeight);
          ctx.fillStyle = '#334155';
          ctx.font = '16px sans-serif';
          ctx.textAlign = 'center';
          ctx.fillText('右上のボタンから画像をアップロード', canvasWidth / 2, canvasHeight / 2);
        }

        // 壁の枠線
        if (showWallLine) {
          ctx.strokeStyle = '#10b981'; ctx.lineWidth = 2; ctx.setLineDash([8, 8]);
          ctx.strokeRect(bounds.left, bounds.top, bounds.right - bounds.left, bounds.bottom - bounds.top);
          ctx.setLineDash([]);
        }

        // 障害物
        obstacles.forEach(o => {
          const isSelected = selectedIds.includes(o.id);
          ctx.fillStyle = isSelected ? 'rgba(239, 68, 68, 0.5)' : 'rgba(245, 158, 11, 0.4)';
          ctx.fillRect(o.x, o.y, o.w, o.h);
          ctx.strokeStyle = isSelected ? '#ef4444' : '#f59e0b';
          ctx.lineWidth = 2;
          ctx.strokeRect(o.x, o.y, o.w, o.h);
        });

        if (previewObs) {
          ctx.fillStyle = 'rgba(16, 185, 129, 0.4)'; ctx.fillRect(previewObs.x, previewObs.y, previewObs.w, previewObs.h);
          ctx.strokeStyle = '#10b981'; ctx.lineWidth = 2; ctx.setLineDash([5, 5]); ctx.strokeRect(previewObs.x, previewObs.y, previewObs.w, previewObs.h); ctx.setLineDash([]);
          const corners = [
            { x: previewObs.x, y: previewObs.y }, { x: previewObs.x + previewObs.w, y: previewObs.y },
            { x: previewObs.x, y: previewObs.y + previewObs.h }, { x: previewObs.x + previewObs.w, y: previewObs.y + previewObs.h }
          ];
          corners.forEach(c => {
            ctx.beginPath(); ctx.arc(c.x, c.y, 8, 0, Math.PI * 2); ctx.fillStyle = '#10b981'; ctx.fill(); ctx.strokeStyle = '#fff'; ctx.lineWidth = 2; ctx.stroke();
          });
        }

        // ワープ
        warps.forEach(w => {
          const isSelected = selectedIds.includes(w.id);
          const strokeIn = isSelected ? '#ef4444' : '#3b82f6';
          const fillIn = isSelected ? 'rgba(239, 68, 68, 0.5)' : 'rgba(59, 130, 246, 0.4)';
          const strokeOut = isSelected ? '#ef4444' : '#f97316';
          const fillOut = isSelected ? 'rgba(239, 68, 68, 0.5)' : 'rgba(249, 115, 22, 0.4)';

          ctx.beginPath(); ctx.moveTo(w.in.x, w.in.y); ctx.lineTo(w.out.x, w.out.y);
          ctx.strokeStyle = isSelected ? '#ef4444' : 'rgba(59, 130, 246, 0.6)'; ctx.lineWidth = 2; ctx.setLineDash([4, 4]); ctx.stroke(); ctx.setLineDash([]);
          ctx.beginPath(); ctx.arc(w.in.x, w.in.y, 20, 0, Math.PI * 2); ctx.fillStyle = fillIn; ctx.fill(); ctx.strokeStyle = strokeIn; ctx.lineWidth = 2; ctx.stroke();
          ctx.fillStyle = '#fff'; ctx.font = '10px sans-serif'; ctx.textAlign = 'center'; ctx.textBaseline = 'middle'; ctx.fillText('IN', w.in.x, w.in.y);
          ctx.beginPath(); ctx.arc(w.out.x, w.out.y, 20, 0, Math.PI * 2); ctx.fillStyle = fillOut; ctx.fill(); ctx.strokeStyle = strokeOut; ctx.lineWidth = 2; ctx.stroke();
          ctx.fillStyle = '#fff'; ctx.fillText('OUT', w.out.x, w.out.y);
        });

        let mainColor = '#06b6d4', glowColor = 'rgba(6, 182, 212, 0.4)';
        if (lineColor === 'white') { mainColor = '#ffffff'; glowColor = 'rgba(255, 255, 255, 0.4)'; }
        else if (lineColor === 'black') { mainColor = '#000000'; glowColor = 'rgba(0, 0, 0, 0.4)'; }

        // 引っ張る目安
        if (showReverseGuide && showTrajectory) {
          const boundsCenter = { x: bounds.left + (bounds.right - bounds.left) / 2, y: bounds.top + (bounds.bottom - bounds.top) / 2 };
          const revRad = (angle + 180) * (Math.PI / 180);
          const revVx = Math.cos(revRad), revVy = Math.sin(revRad);
          const distToEdge = (x, y, vx, vy, b) => {
            let tx = Infinity, ty = Infinity;
            if (vx > 0) tx = (b.right - x) / vx; if (vx < 0) tx = (b.left - x) / vx;
            if (vy > 0) ty = (b.bottom - y) / vy; if (vy < 0) ty = (b.top - y) / vy;
            return Math.min(tx, ty);
          };
          const d1 = distToEdge(boundsCenter.x, boundsCenter.y, -revVx, -revVy, bounds);
          const pt1 = { x: boundsCenter.x - revVx * d1, y: boundsCenter.y - revVy * d1 }; // 正方向
          const d2 = distToEdge(boundsCenter.x, boundsCenter.y, revVx, revVy, bounds);
          const pt2 = { x: boundsCenter.x + revVx * d2, y: boundsCenter.y + revVy * d2 }; // 逆方向

          ctx.beginPath(); ctx.moveTo(pt1.x, pt1.y); ctx.lineTo(pt2.x, pt2.y);
          ctx.strokeStyle = '#ef4444'; ctx.lineWidth = 3; ctx.stroke();
          // ★ 赤丸を pt1 (飛んでいく方向の端) に描画するように変更
          ctx.beginPath(); ctx.arc(pt1.x, pt1.y, 5, 0, Math.PI * 2); ctx.fillStyle = '#dc2626'; ctx.fill(); ctx.strokeStyle = '#ffffff'; ctx.lineWidth = 2; ctx.stroke();
        }

        // 軌道
        const path = calculatePath();
        if (path.length > 1) {
          if (showBand) {
            ctx.beginPath(); ctx.moveTo(path[0].x, path[0].y);
            for (let i = 1; i < path.length; i++) {
              if (path[i].type === 'warpOut') ctx.moveTo(path[i].x, path[i].y);
              else ctx.lineTo(path[i].x, path[i].y);
            }
            ctx.strokeStyle = glowColor; ctx.lineWidth = 20; ctx.lineCap = 'round'; ctx.lineJoin = 'round'; ctx.stroke();
          }

          ctx.beginPath(); ctx.moveTo(path[0].x, path[0].y);
          for (let i = 1; i < path.length; i++) {
            if (path[i].type === 'warpOut') ctx.moveTo(path[i].x, path[i].y);
            else ctx.lineTo(path[i].x, path[i].y);
          }
          ctx.strokeStyle = mainColor; ctx.lineWidth = 4; ctx.lineCap = 'round'; ctx.lineJoin = 'round'; ctx.stroke();
        }

        // 反射回数
        let bounceCount = 0;
        path.forEach((p, i) => {
          if (i > 0 && p.type !== 'warpIn' && p.type !== 'warpOut') {
            bounceCount++;
            const offset = 14;
            const textX = p.x - p.nx * offset; const textY = p.y - p.ny * offset;
            ctx.beginPath(); ctx.arc(textX, textY, 8, 0, Math.PI * 2); ctx.fillStyle = lineColor === 'white' ? '#e2e8f0' : '#1e293b'; ctx.fill();
            ctx.strokeStyle = mainColor; ctx.lineWidth = 1.5; ctx.stroke();
            ctx.fillStyle = lineColor === 'white' ? '#0f172a' : '#f8fafc'; ctx.font = 'bold 11px sans-serif'; ctx.textAlign = 'center'; ctx.textBaseline = 'middle'; ctx.fillText(bounceCount.toString(), textX, textY);
          }
        });

        // スタート地点
        ctx.beginPath(); ctx.arc(startPoint.x, startPoint.y, 5, 0, Math.PI * 2); ctx.fillStyle = mainColor; ctx.fill(); ctx.strokeStyle = lineColor === 'white' ? '#000000' : '#ffffff'; ctx.lineWidth = 2; ctx.stroke();
        ctx.beginPath(); ctx.arc(startPoint.x, startPoint.y, 18, 0, Math.PI * 2); ctx.strokeStyle = mainColor; ctx.lineWidth = 2; ctx.setLineDash([4, 4]); ctx.stroke(); ctx.setLineDash([]);

      }, [image, startPoint, angle, wallPercents, maxBounces, showReverseGuide, showBand, showTrajectory, showWallLine, lineColor, obstacles, previewObs, warps, selectedIds, viewWidth, viewHeight, calculatePath]);

      const isSmartphone = wallPercents.top === defaultWalls.top && wallPercents.bottom === defaultWalls.bottom && wallPercents.left === defaultWalls.left && wallPercents.right === defaultWalls.right;
      const isTablet = wallPercents.top === tabletWalls.top && wallPercents.bottom === tabletWalls.bottom && wallPercents.left === tabletWalls.left && wallPercents.right === tabletWalls.right;

      return (
        <div className="relative h-[100dvh] bg-slate-950 text-slate-200 flex flex-col font-sans select-none overflow-hidden sm:max-w-md sm:mx-auto sm:border-x sm:border-slate-800">
          
          <header className="flex items-center justify-between p-3 bg-slate-900 border-b border-slate-800 shrink-0">
            <h1 className="text-sm font-bold text-slate-100 tracking-wide flex items-center gap-1.5">
              <span className="text-teal-400"><IconCrosshair /></span> モンストガイドマスター
            </h1>
            <div className="flex items-center gap-2">
              <div className="flex items-center bg-slate-800 rounded-lg p-0.5 border border-slate-700">
                <button onClick={handleUndo} disabled={historyIndex <= 0} className={`p-1.5 rounded transition-colors ${historyIndex > 0 ? 'text-slate-200 active:bg-slate-700' : 'text-slate-600 cursor-not-allowed'}`}><IconUndo /></button>
                <div className="w-[1px] h-4 bg-slate-700 mx-0.5"></div>
                <button onClick={handleRedo} disabled={historyIndex >= history.length - 1} className={`p-1.5 rounded transition-colors ${historyIndex < history.length - 1 ? 'text-slate-200 active:bg-slate-700' : 'text-slate-600 cursor-not-allowed'}`}><IconRedo /></button>
              </div>
              <input type="file" accept="image/*" className="hidden" ref={fileInputRef} onChange={handleImageUpload} />
              <button onClick={() => fileInputRef.current?.click()} className="flex items-center gap-1 bg-teal-500/20 text-teal-400 px-3 py-1.5 rounded-full text-xs font-medium active:bg-teal-500/30 border border-teal-500/30"><IconUpload /> 画像</button>
            </div>
          </header>

          <main className="flex-none w-full flex items-center justify-center p-3 bg-slate-950 overflow-hidden relative" style={{ height: '45vh' }}>
            <canvas 
              ref={canvasRef} 
              onTouchStart={handleTouchStart} 
              onTouchMove={handleTouchMove} 
              onTouchEnd={handleEnd} 
              onTouchCancel={handleEnd} 
              onMouseDown={handleMouseDown} 
              onMouseMove={handleMouseMove} 
              onMouseUp={handleEnd} 
              onMouseLeave={handleEnd} 
              className="cursor-crosshair rounded-md shadow-[0_0_20px_rgba(0,0,0,0.5)] bg-slate-900 border border-slate-800 w-auto h-auto max-w-full max-h-full" 
              style={{ aspectRatio: `${viewWidth} / ${viewHeight}` }} 
            />
          </main>

          <div className="bg-slate-900 border-t border-slate-800 shrink-0 pb-safe flex flex-col flex-1 min-h-0">
            <div className="flex border-b border-slate-800 shrink-0">
              <button className={`flex-1 py-3 text-xs font-bold tracking-wider ${activeTab === 'aim' ? 'text-teal-400 border-b-2 border-teal-400 bg-slate-800/50' : 'text-slate-500'}`} onClick={() => setActiveTab('aim')}>射出設定</button>
              <button className={`flex-1 py-3 text-xs font-bold tracking-wider ${activeTab === 'walls' ? 'text-teal-400 border-b-2 border-teal-400 bg-slate-800/50' : 'text-slate-500'}`} onClick={() => setActiveTab('walls')}>壁設定</button>
              <button className={`flex-1 py-3 text-xs font-bold tracking-wider ${activeTab === 'obstacles' ? 'text-amber-400 border-b-2 border-amber-400 bg-slate-800/50' : 'text-slate-500'}`} onClick={() => setActiveTab('obstacles')}>障害物</button>
              <button className={`flex-1 py-3 text-xs font-bold tracking-wider ${activeTab === 'save' ? 'text-indigo-400 border-b-2 border-indigo-400 bg-slate-800/50' : 'text-slate-500'}`} onClick={() => setActiveTab('save')}>💾 保存</button>
            </div>

            <div className="p-4 flex-1 overflow-y-auto">
              
              {activeTab === 'aim' && (
                <div className="space-y-4">
                  <div className="flex items-center justify-between">
                    <span className="text-xs text-slate-400">発射角度 (手動調整)</span>
                    <div className="bg-slate-950 border border-slate-700 rounded px-3 py-1 font-mono text-sm">{angle.toFixed(1)}°</div>
                  </div>
                  <input type="range" min="0" max="360" step="0.1" value={angle} onChange={(e) => setAngle(parseFloat(e.target.value))} className="w-full accent-teal-500" />
                  
                  <div className="flex gap-2">
                    <button onClick={() => setAngle(a => (a - 1 + 360) % 360)} className="flex-1 bg-slate-800/80 hover:bg-slate-700 py-2.5 rounded-md text-[13px] font-medium active:bg-slate-700 border border-slate-700/50">-1°</button>
                    <button onClick={() => setAngle(a => (a - 0.1 + 360) % 360)} className="flex-1 bg-slate-800/80 hover:bg-slate-700 py-2.5 rounded-md text-[13px] font-medium active:bg-slate-700 border border-slate-700/50">-0.1°</button>
                    <button onClick={() => setAngle(a => (a + 0.1) % 360)} className="flex-1 bg-slate-800/80 hover:bg-slate-700 py-2.5 rounded-md text-[13px] font-medium active:bg-slate-700 border border-slate-700/50">+0.1°</button>
                    <button onClick={() => setAngle(a => (a + 1) % 360)} className="flex-1 bg-slate-800/80 hover:bg-slate-700 py-2.5 rounded-md text-[13px] font-medium active:bg-slate-700 border border-slate-700/50">+1°</button>
                  </div>
                  
                  <div className="flex gap-1.5 sm:gap-2">
                    <button onClick={() => setShowTrajectory(!showTrajectory)} className={`flex-1 py-2.5 rounded-md text-[11px] font-medium border ${showTrajectory ? 'bg-teal-500/20 text-teal-400 border-teal-500/50' : 'bg-slate-800/80 text-slate-400 border-slate-700/50'}`}>線 {showTrajectory ? 'ON' : 'OFF'}</button>
                    <button onClick={() => setShowBand(!showBand)} className={`flex-1 py-2.5 rounded-md text-[11px] font-medium border ${showBand ? 'bg-teal-500/20 text-teal-400 border-teal-500/50' : 'bg-slate-800/80 text-slate-400 border-slate-700/50'}`}>幅 {showBand ? 'ON' : 'OFF'}</button>
                    <button onClick={() => setShowReverseGuide(!showReverseGuide)} className={`flex-1 py-2.5 rounded-md text-[11px] font-medium border ${showReverseGuide ? 'bg-red-500/20 text-red-400 border-red-500/50' : 'bg-slate-800/80 text-slate-400 border-slate-700/50'}`}>目安 {showReverseGuide ? 'ON' : 'OFF'}</button>
                    <button onClick={() => setMaxBounces((b) => (b >= 15 ? 1 : b + 1))} className="flex-[1.1] py-2.5 rounded-md text-[11px] font-medium border bg-slate-800/80 text-slate-200 border-slate-700/50">反射 {maxBounces}回</button>
                    <button onClick={() => { const colors = ['white', 'cyan', 'black']; setLineColor(colors[(colors.indexOf(lineColor) + 1) % colors.length]); }} className="flex-1 py-2.5 rounded-md text-[11px] font-medium border bg-slate-800/80 text-slate-200 border-slate-700/50 flex items-center justify-center gap-1">
                      {lineColor === 'white' ? '白' : lineColor === 'cyan' ? 'シアン' : '黒'}
                      <div className={`w-1.5 h-1.5 rounded-full ${lineColor === 'cyan' ? 'bg-cyan-400' : lineColor === 'white' ? 'bg-white' : 'bg-black border border-slate-500'}`} />
                    </button>
                  </div>

                  <button onClick={() => setIsMoveMode(!isMoveMode)} className={`w-full py-3 mt-1 rounded-lg text-[13px] font-bold flex items-center justify-center gap-2 transition-colors border ${isMoveMode ? 'bg-amber-500/20 text-amber-400 border-amber-500/50 shadow-[0_0_10px_rgba(245,158,11,0.2)]' : 'bg-slate-800/80 text-slate-300 border-slate-700/80 hover:bg-slate-800'}`}>
                    <IconHand size={18} /> 画面移動モード：{isMoveMode ? 'ON (移動・ズーム可)' : 'OFF (射出可能)'}
                  </button>
                </div>
              )}

              {activeTab === 'walls' && (
                <div className="space-y-4">
                  <div className="flex gap-2 pb-2 border-b border-slate-800">
                    <button onClick={() => setWallPercents(defaultWalls)} className={`flex-1 py-1.5 rounded text-[11px] font-bold border transition-colors ${isSmartphone ? 'bg-emerald-500/20 text-emerald-400 border-emerald-500/40' : 'bg-slate-800 text-slate-400 border-slate-700'}`}>📱 スマホ（初期）</button>
                    <button onClick={() => setWallPercents(tabletWalls)} className={`flex-1 py-1.5 rounded text-[11px] font-bold border transition-colors ${isTablet ? 'bg-emerald-500/20 text-emerald-400 border-emerald-500/40' : 'bg-slate-800 text-slate-400 border-slate-700'}`}>タブレット/iPad</button>
                  </div>
                  <div className="flex justify-between items-center mb-2">
                    <span className="text-xs text-slate-400">壁の範囲設定 (%)</span>
                    <div className="flex gap-2">
                      <button onClick={() => setShowWallLine(!showWallLine)} className={`text-[10px] px-2 py-1 rounded border ${showWallLine ? 'bg-emerald-500/20 text-emerald-400 border-emerald-500/30' : 'bg-slate-800 text-slate-500 border-slate-700'}`}>枠線 {showWallLine ? 'ON' : 'OFF'}</button>
                      <button onClick={() => setWallPercents(defaultWalls)} className="flex items-center gap-1 text-[10px] text-slate-400 bg-slate-800 px-2 py-1 rounded border border-slate-700"><IconRefresh /> リセット</button>
                    </div>
                  </div>
                  <div className="grid grid-cols-2 gap-x-4 gap-y-4">
                    {['top', 'bottom', 'left', 'right'].map((dir) => (
                      <div key={dir} className="flex flex-col gap-1">
                        <div className="flex justify-between text-[10px]">
                          <span className="uppercase text-slate-500">{dir === 'top' ? '上' : dir === 'bottom' ? '下' : dir === 'left' ? '左' : '右'}</span>
                          <span className="text-slate-300">{wallPercents[dir]}%</span>
                        </div>
                        <input type="range" min="0" max="45" step="1" value={wallPercents[dir]} onChange={(e) => setWallPercents(p => ({...p, [dir]: parseInt(e.target.value)}))} className="w-full accent-emerald-500 h-1 bg-slate-800 rounded-full appearance-none [&::-webkit-slider-thumb]:appearance-none [&::-webkit-slider-thumb]:w-3 [&::-webkit-slider-thumb]:h-3 [&::-webkit-slider-thumb]:bg-emerald-400 [&::-webkit-slider-thumb]:rounded-full" />
                      </div>
                    ))}
                  </div>
                </div>
              )}

              {activeTab === 'obstacles' && (
                <div className="space-y-4">
                  <div className="flex gap-2 p-1 bg-slate-950 rounded-lg border border-slate-800">
                    <button onClick={() => setObsMode('edit')} className={`flex-1 py-2 text-xs font-bold rounded-md transition-colors ${obsMode === 'edit' ? 'bg-amber-500 text-amber-950' : 'text-slate-400'}`}>🔧 配置・編集</button>
                    <button onClick={() => { setObsMode('delete'); setPreviewObs(null); setSelectedIds([]); }} className={`flex-1 py-2 text-xs font-bold rounded-md transition-colors ${obsMode === 'delete' ? 'bg-red-500 text-white' : 'text-slate-400'}`}>🗑️ 選択・削除</button>
                  </div>
                  {obsMode === 'edit' ? (
                    <div className="space-y-3">
                      <div className="flex gap-2">
                        <button onClick={() => setObsType('block')} className={`flex-1 py-2 rounded text-xs border ${obsType === 'block' ? 'bg-amber-500/20 border-amber-500 text-amber-400' : 'bg-slate-800 border-slate-700 text-slate-400'}`}>🟥 ブロック</button>
                        <button onClick={() => setObsType('warp')} className={`flex-1 py-2 rounded text-xs border ${obsType === 'warp' ? 'bg-blue-500/20 border-blue-500 text-blue-400' : 'bg-slate-800 border-slate-700 text-slate-400'}`}>🌀 ワープ</button>
                      </div>
                      <p className="text-xs text-slate-400">画面タップで{obsType === 'block' ? 'ブロック' : 'ワープ(IN/OUT)'}を配置します。四隅をドラッグでサイズ調整できます。</p>
                      {previewObs && (
                        <button onClick={() => { setObstacles([...obstacles, previewObs]); setPreviewObs(null); pushHistoryDebounced(); }} className="w-full py-3 bg-emerald-600 hover:bg-emerald-500 text-white text-sm font-bold rounded-lg flex items-center justify-center gap-2 shadow-[0_0_15px_rgba(16,185,129,0.4)] animate-pulse">
                          <IconCheck /> 配置を確定する
                        </button>
                      )}
                    </div>
                  ) : (
                    <div className="space-y-3">
                      <p className="text-xs text-slate-400">消したいブロックやワープをタップして赤く選択してください。</p>
                      <div className="flex gap-2">
                        <button onClick={() => { setObstacles(obstacles.filter(o => !selectedIds.includes(o.id))); setWarps(warps.filter(w => !selectedIds.includes(w.id))); setSelectedIds([]); pushHistoryDebounced(); }} disabled={selectedIds.length === 0} className={`flex-1 py-2 rounded text-xs font-bold transition-colors ${selectedIds.length > 0 ? 'bg-red-600 text-white active:bg-red-700' : 'bg-slate-800 text-slate-600'}`}>選択中を削除 ({selectedIds.length})</button>
                        <button onClick={() => { setObstacles([]); setWarps([]); setSelectedIds([]); pushHistoryDebounced(); }} className="flex-1 py-2 rounded text-xs font-bold bg-slate-800 text-red-400 border border-red-900/30 active:bg-slate-700">すべて削除</button>
                      </div>
                    </div>
                  )}
                </div>
              )}

              {activeTab === 'save' && (
                <div className="space-y-4">
                  <div className="space-y-2">
                    <label className="text-xs text-slate-400">ステージ配置に名前を付けて保存</label>
                    <div className="flex gap-2">
                      <input type="text" value={saveName} onChange={(e) => setSaveName(e.target.value)} placeholder="例：でてぃあかるステージ２" className="flex-1 bg-slate-950 border border-slate-700 rounded px-3 py-2 text-xs text-slate-100 focus:outline-none focus:border-indigo-500" />
                      <button onClick={handleSaveStage} disabled={!saveName.trim()} className={`px-4 py-2 rounded text-xs font-bold flex items-center gap-1 transition-all ${saveName.trim() ? 'bg-indigo-600 text-white active:bg-indigo-700' : 'bg-slate-800 text-slate-500 border border-slate-700 cursor-not-allowed'}`}><IconSave /> 保存</button>
                    </div>
                  </div>
                  <div className="pt-2 border-t border-slate-800 space-y-2">
                    <span className="text-xs text-slate-400">保存済みリスト ({savedStages.length})</span>
                    {savedStages.length === 0 ? (
                      <p className="text-[11px] text-slate-500 py-4 text-center">保存された配置はありません</p>
                    ) : (
                      <div className="space-y-2 max-h-48 overflow-y-auto pr-1">
                        {savedStages.map((stage) => (
                          <div key={stage.id} className="flex items-center justify-between bg-slate-950 p-2.5 rounded-lg border border-slate-800">
                            <div>
                              <div className="text-xs font-bold text-slate-200">{stage.name}</div>
                              <div className="text-[10px] text-slate-500">{stage.date} • ブロック:{stage.obstacles?.length || 0} / ワープ:{stage.warps?.length || 0}</div>
                            </div>
                            <div className="flex gap-1.5">
                              <button onClick={() => handleLoadStage(stage)} className="px-2.5 py-1 rounded text-[11px] font-bold bg-indigo-500/20 text-indigo-300 border border-indigo-500/40 active:bg-indigo-500/30">読み込む</button>
                              <button onClick={() => handleDeleteStage(stage.id)} className="p-1 rounded text-slate-500 hover:text-red-400 active:bg-slate-800"><IconTrash /></button>
                            </div>
                          </div>
                        ))}
                      </div>
                    )}
                  </div>
                </div>
              )}
            </div>
          </div>
        </div>
      );
    };

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
  </script>
</body>
</html>
