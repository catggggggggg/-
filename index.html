import React, { useState, useRef, useEffect, useCallback } from 'react';
import { Camera, RefreshCw, Upload, Crosshair, Hand } from 'lucide-react';

const App = () => {
  const [image, setImage] = useState(null);
  const [startPoint, setStartPoint] = useState({ x: 195, y: 550 });
  const [angle, setAngle] = useState(45);
  const [isMoveMode, setIsMoveMode] = useState(false); // ★移動モードの状態を追加

  // --- 追加: ズームしても絶対に右下に追従するボタンスタイル用の状態 ---
  const [btnStyle, setBtnStyle] = useState({
    position: 'fixed',
    right: '24px',
    bottom: '24px',
    zIndex: 9999,
  });

  // App Settings
  const [maxBounces, setMaxBounces] = useState(3);
  const [showReverseGuide, setShowReverseGuide] = useState(true);
  const [showBand, setShowBand] = useState(true);
  const [showWallLine, setShowWallLine] = useState(true);
  const [lineColor, setLineColor] = useState('cyan'); // 'cyan', 'white', 'black'

  // Wall Settings (初期値はスマホ目安)
  const defaultWalls = { top: 19, bottom: 33, left: 5, right: 5 };
  const [wallPercents, setWallPercents] = useState(defaultWalls);

  const [activeTab, setActiveTab] = useState('aim'); // 'aim' or 'walls'
  const [dragMode, setDragMode] = useState(null); // 'origin' or 'angle'

  // Refs
  const canvasRef = useRef(null);
  const fileInputRef = useRef(null);

  // Fixed Canvas resolution
  const canvasWidth = 390;
  const canvasHeight = 844;

  const bounds = {
    left: canvasWidth * (wallPercents.left / 100),
    right: canvasWidth * (1 - wallPercents.right / 100),
    top: canvasHeight * (wallPercents.top / 100),
    bottom: canvasHeight * (1 - wallPercents.bottom / 100),
  };

  // 枠線から少し外側（マージン）を残してクロップするための計算
  const cropMargin = 20; 
  const viewBounds = {
    left: Math.max(0, bounds.left - cropMargin),
    right: Math.min(canvasWidth, bounds.right + cropMargin),
    top: Math.max(0, bounds.top - cropMargin),
    bottom: Math.min(canvasHeight, bounds.bottom + cropMargin),
  };
  const viewWidth = viewBounds.right - viewBounds.left;
  const viewHeight = viewBounds.bottom - viewBounds.top;

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

  const updateAngleFromCoords = (coords) => {
    if (!coords) return;
    const dx = coords.x - startPoint.x;
    const dy = coords.y - startPoint.y;
    let newAngle = Math.atan2(dy, dx) * (180 / Math.PI);
    if (newAngle < 0) newAngle += 360;
    setAngle(newAngle);
  };

  const startInteraction = (coords) => {
    if (!coords) return;
    const dist = Math.hypot(coords.x - startPoint.x, coords.y - startPoint.y);
    // 判定エリアを広げて掴みやすく変更 (40 -> 60)
    if (dist < 60) {
      setDragMode('origin');
    } else {
      setDragMode('angle');
      updateAngleFromCoords(coords);
    }
  };

  const moveInteraction = (coords) => {
    if (!coords) return;
    if (dragMode === 'origin') {
      const bounds = {
        left: canvasWidth * (wallPercents.left / 100),
        right: canvasWidth * (1 - wallPercents.right / 100),
        top: canvasHeight * (wallPercents.top / 100),
        bottom: canvasHeight * (1 - wallPercents.bottom / 100),
      };
      // Clamp drag strictly to bounds
      const clampedX = Math.max(bounds.left, Math.min(coords.x, bounds.right));
      const clampedY = Math.max(bounds.top, Math.min(coords.y, bounds.bottom));
      setStartPoint({ x: clampedX, y: clampedY });
    } else if (dragMode === 'angle') {
      updateAngleFromCoords(coords);
    }
  };

  const handleTouchStart = (e) => {
    if (isMoveMode) return; // ★移動モード中は操作を無視
    // Only process single touches, ignore multi-touch
    if (e.touches.length === 1) {
      const touch = e.touches[0];
      startInteraction(getCanvasCoords(touch.clientX, touch.clientY));
    } else {
      setDragMode(null);
    }
  };

  const handleTouchMove = (e) => {
    if (isMoveMode) return; // ★移動モード中は操作を無視
    if (e.touches.length === 1 && dragMode) {
      const touch = e.touches[0];
      moveInteraction(getCanvasCoords(touch.clientX, touch.clientY));
    }
  };

  const handleEnd = () => {
    setDragMode(null);
  };

  const handleMouseDown = (e) => { if (!isMoveMode) startInteraction(getCanvasCoords(e.clientX, e.clientY)); };
  const handleMouseMove = (e) => { if (!isMoveMode && dragMode) moveInteraction(getCanvasCoords(e.clientX, e.clientY)); };

  // --- 追加: ズーム時の画面表示領域(Visual Viewport)を監視してボタンを張り付ける処理 ---
  useEffect(() => {
    const vv = window.visualViewport;
    if (!vv) return;

    const updatePosition = () => {
      const scale = vv.scale;
      // 画面の端から24pxの余白を維持（ズーム倍率で割ることで見た目のサイズを一定に）
      const padding = 24 / scale;
      
      // 今見ている画面(視界)の右下の座標をリアルタイム計算
      const left = vv.offsetLeft + vv.width - padding;
      const top = vv.offsetTop + vv.height - padding;

      setBtnStyle({
        position: 'fixed',
        left: `${left}px`,
        top: `${top}px`,
        // 倍率の逆数(1/scale)をかけてボタンの巨大化を防ぎ、右下基準で配置する
        transform: `translate(-100%, -100%) scale(${1 / scale})`,
        transformOrigin: 'bottom right',
        zIndex: 9999,
      });
    };

    vv.addEventListener('resize', updatePosition, { passive: true });
    vv.addEventListener('scroll', updatePosition, { passive: true });
    updatePosition(); // 初期計算

    return () => {
      vv.removeEventListener('resize', updatePosition);
      vv.removeEventListener('scroll', updatePosition);
    };
  }, []);

  // --- 1本指の時だけスクロールを止め、2本指以上の時はブラウザのズーム/移動を許可する ---
  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;

    const preventSingleTouch = (e) => {
      if (isMoveMode) return; // ★移動モード中はブラウザのスクロールを止めない

      if (e.touches.length === 1) {
        if (e.cancelable) {
          e.preventDefault(); // 1本指の時は画面スクロールを止めて射出操作に集中
        }
      }
    };

    // passive: false でないと preventDefault() が効かないため、直接イベントリスナーを追加
    canvas.addEventListener('touchstart', preventSingleTouch, { passive: false });
    canvas.addEventListener('touchmove', preventSingleTouch, { passive: false });

    return () => {
      canvas.removeEventListener('touchstart', preventSingleTouch);
      canvas.removeEventListener('touchmove', preventSingleTouch);
    };
  }, [isMoveMode]); // ★isMoveModeを依存関係に追加

  // --- EXACT Raycasting Logic with Pre-bounce ---
  const calculatePath = useCallback(() => {
    const path = [{ x: startPoint.x, y: startPoint.y, nx: 0, ny: 0 }];
    
    let rad = angle * (Math.PI / 180);
    let vx = Math.cos(rad);
    let vy = Math.sin(rad);

    let currentX = startPoint.x;
    let currentY = startPoint.y;

    // --- PRE-BOUNCE LOGIC (For corners / walls) ---
    const EPSILON = 0.5;
    
    if (currentX <= bounds.left + EPSILON && vx < 0) vx = -vx;
    if (currentX >= bounds.right - EPSILON && vx > 0) vx = -vx;
    if (currentY <= bounds.top + EPSILON && vy < 0) vy = -vy;
    if (currentY >= bounds.bottom - EPSILON && vy > 0) vy = -vy;

    for (let i = 0; i < maxBounces; i++) {
      let tMin = Infinity;
      let nextX = currentX;
      let nextY = currentY;
      let hitNormalX = 0;
      let hitNormalY = 0;

      // Right Wall
      if (vx > 0) {
        let t = (bounds.right - currentX) / vx;
        if (t > 0.1 && t < tMin) {
          tMin = t;
          nextX = bounds.right;
          nextY = currentY + t * vy;
          hitNormalX = -1; hitNormalY = 0;
        }
      }
      // Left Wall
      if (vx < 0) {
        let t = (bounds.left - currentX) / vx;
        if (t > 0.1 && t < tMin) {
          tMin = t;
          nextX = bounds.left;
          nextY = currentY + t * vy;
          hitNormalX = 1; hitNormalY = 0;
        }
      }
      // Bottom Wall
      if (vy > 0) {
        let t = (bounds.bottom - currentY) / vy;
        if (t > 0.1 && t < tMin) {
          // Check if intersection point is strictly within horizontal bounds
          let tempX = currentX + t * vx;
          if (tempX >= bounds.left - 0.1 && tempX <= bounds.right + 0.1) {
            tMin = t;
            nextX = tempX;
            nextY = bounds.bottom;
            hitNormalX = 0; hitNormalY = -1;
          }
        }
      }
      // Top Wall
      if (vy < 0) {
        let t = (bounds.top - currentY) / vy;
        if (t > 0.1 && t < tMin) {
          let tempX = currentX + t * vx;
          if (tempX >= bounds.left - 0.1 && tempX <= bounds.right + 0.1) {
            tMin = t;
            nextX = tempX;
            nextY = bounds.top;
            hitNormalX = 0; hitNormalY = 1;
          }
        }
      }

      if (tMin === Infinity) break; // Error fallback

      path.push({ x: nextX, y: nextY, nx: hitNormalX, ny: hitNormalY });

      // Reflect
      if (hitNormalX !== 0) vx = -vx;
      if (hitNormalY !== 0) vy = -vy;

      currentX = nextX;
      currentY = nextY;
    }

    return path;
  }, [startPoint, angle, wallPercents, maxBounces, canvasWidth, canvasHeight]);

  // Main Render Loop
  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;
    const ctx = canvas.getContext('2d');

    // 高解像度（Retina）ディスプレイ対応で画質を向上
    const dpr = window.devicePixelRatio || 1;
    canvas.width = viewWidth * dpr;
    canvas.height = viewHeight * dpr;

    ctx.scale(dpr, dpr);
    
    // クロップ範囲に合わせて座標系をシフト
    ctx.translate(-viewBounds.left, -viewBounds.top);

    // Clear
    ctx.clearRect(0, 0, canvasWidth, canvasHeight);

    // Draw Image (Fixed scale to fit)
    if (image) {
      ctx.save();
      const imgAspect = image.width / image.height;
      const canvasAspect = canvasWidth / canvasHeight;
      let drawW, drawH;
      
      if (imgAspect > canvasAspect) {
        drawW = canvasWidth;
        drawH = canvasWidth / imgAspect;
      } else {
        drawH = canvasHeight;
        drawW = canvasHeight * imgAspect;
      }
      
      ctx.translate(canvasWidth / 2, canvasHeight / 2);
      ctx.drawImage(image, -drawW / 2, -drawH / 2, drawW, drawH);
      ctx.restore();
    } else {
      ctx.fillStyle = '#0f172a'; // slate-900
      ctx.fillRect(0, 0, canvasWidth, canvasHeight);
      ctx.fillStyle = '#334155';
      ctx.font = '16px sans-serif';
      ctx.textAlign = 'center';
      ctx.fillText('右上のボタンから画像をアップロード', canvasWidth / 2, canvasHeight / 2);
    }

    // Draw Wall bounds (Green dashed)
    if (showWallLine) {
      ctx.strokeStyle = '#10b981'; // emerald-500
      ctx.lineWidth = 2;
      ctx.setLineDash([8, 8]);
      ctx.strokeRect(bounds.left, bounds.top, bounds.right - bounds.left, bounds.bottom - bounds.top);
      ctx.setLineDash([]); // Reset
    }

    // Colors
    let mainColor = '#06b6d4'; // cyan
    let glowColor = 'rgba(6, 182, 212, 0.4)';
    if (lineColor === 'white') {
      mainColor = '#ffffff';
      glowColor = 'rgba(255, 255, 255, 0.4)';
    } else if (lineColor === 'black') {
      mainColor = '#000000';
      glowColor = 'rgba(0, 0, 0, 0.4)';
    }

    // --- Reverse Guide Line (Pull Indicator) ---
    if (showReverseGuide) {
      // 枠線の中心
      const boundsCenter = {
        x: bounds.left + (bounds.right - bounds.left) / 2,
        y: bounds.top + (bounds.bottom - bounds.top) / 2
      };

      // 逆方向のベクトル
      const revRad = (angle + 180) * (Math.PI / 180);
      const revVx = Math.cos(revRad);
      const revVy = Math.sin(revRad);

      // 中心から枠線の端までの長さを計算
      const distToEdge = (x, y, vx, vy, b) => {
        let tx = Infinity, ty = Infinity;
        if (vx > 0) tx = (b.right - x) / vx;
        if (vx < 0) tx = (b.left - x) / vx;
        if (vy > 0) ty = (b.bottom - y) / vy;
        if (vy < 0) ty = (b.top - y) / vy;
        return Math.min(tx, ty);
      };

      // 中心から正方向（発射方向）への距離
      const d1 = distToEdge(boundsCenter.x, boundsCenter.y, -revVx, -revVy, bounds);
      const pt1 = {
        x: boundsCenter.x - revVx * d1,
        y: boundsCenter.y - revVy * d1
      };

      // 中心から逆方向への距離
      const d2 = distToEdge(boundsCenter.x, boundsCenter.y, revVx, revVy, bounds);
      const pt2 = {
        x: boundsCenter.x + revVx * d2,
        y: boundsCenter.y + revVy * d2
      };

      ctx.beginPath();
      ctx.moveTo(pt1.x, pt1.y);
      ctx.lineTo(pt2.x, pt2.y);
      ctx.strokeStyle = '#ef4444'; // red-500 (不透明にして濃くしました)
      ctx.lineWidth = 3;
      ctx.stroke();

      // 赤丸を引っ張る始点（逆方向の端 = pt2）に描画
      ctx.beginPath();
      ctx.arc(pt2.x, pt2.y, 10, 0, Math.PI * 2); // 5から10に大きくしました
      ctx.fillStyle = '#dc2626'; // red-600 (少し濃い赤)
      ctx.fill();
      ctx.strokeStyle = '#ffffff';
      ctx.lineWidth = 2;
      ctx.stroke();
    }

    // --- Draw Trajectory ---
    const path = calculatePath();

    if (path.length > 1) {
      if (showBand) {
        ctx.beginPath();
        ctx.moveTo(path[0].x, path[0].y);
        for (let i = 1; i < path.length; i++) ctx.lineTo(path[i].x, path[i].y);
        ctx.strokeStyle = glowColor;
        ctx.lineWidth = 20; // 太くした帯
        ctx.lineCap = 'round';
        ctx.lineJoin = 'round';
        ctx.stroke();
      }

      ctx.beginPath();
      ctx.moveTo(path[0].x, path[0].y);
      for (let i = 1; i < path.length; i++) ctx.lineTo(path[i].x, path[i].y);
      ctx.strokeStyle = mainColor;
      ctx.lineWidth = 4; // 太くしたメインライン
      ctx.lineCap = 'round';
      ctx.lineJoin = 'round';
      ctx.stroke();
    }

    // --- 反射回数のバッジを描画 ---
    path.forEach((p, i) => {
      if (i > 0) {
        // 法線ベクトル（nx, ny）の逆方向にオフセットして壁の外側に配置
        const offset = 14; 
        const textX = p.x - p.nx * offset;
        const textY = p.y - p.ny * offset;
        
        // バッジの背景丸
        ctx.beginPath();
        ctx.arc(textX, textY, 8, 0, Math.PI * 2);
        ctx.fillStyle = lineColor === 'white' ? '#e2e8f0' : '#1e293b'; 
        ctx.fill();
        ctx.strokeStyle = mainColor;
        ctx.lineWidth = 1.5;
        ctx.stroke();

        // 番号テキスト
        ctx.fillStyle = lineColor === 'white' ? '#0f172a' : '#f8fafc';
        ctx.font = 'bold 11px sans-serif';
        ctx.textAlign = 'center';
        ctx.textBaseline = 'middle';
        ctx.fillText(i.toString(), textX, textY);
      }
    });

    // Start Point Node
    ctx.beginPath();
    ctx.arc(startPoint.x, startPoint.y, 10, 0, Math.PI * 2);
    ctx.fillStyle = mainColor;
    ctx.fill();
    ctx.strokeStyle = lineColor === 'white' ? '#000000' : '#ffffff';
    ctx.lineWidth = 2;
    ctx.stroke();

  }, [image, startPoint, angle, wallPercents, maxBounces, showReverseGuide, showBand, showWallLine, lineColor, canvasWidth, canvasHeight, calculatePath]);

  return (
    <div className="relative h-[100dvh] bg-slate-950 text-slate-200 flex flex-col font-sans select-none overflow-hidden sm:max-w-md sm:mx-auto sm:border-x sm:border-slate-800">
      
      {/* Header */}
      <header className="flex items-center justify-between p-3 bg-slate-900 border-b border-slate-800 shrink-0">
        <h1 className="text-sm font-bold text-slate-100 tracking-wide flex items-center gap-1.5">
          <Crosshair size={16} className="text-teal-400" />
          壁反射
        </h1>
        
        <div className="flex items-center gap-2">
          <input 
            type="file" 
            accept="image/*" 
            className="hidden" 
            ref={fileInputRef} 
            onChange={handleImageUpload}
          />
          <button 
            onClick={() => fileInputRef.current?.click()}
            className="flex items-center gap-1 bg-teal-500/20 text-teal-400 px-3 py-1.5 rounded-full text-xs font-medium active:bg-teal-500/30 transition-colors border border-teal-500/30"
          >
            <Upload size={14} /> 画像
          </button>
        </div>
      </header>

      {/* 画面移動（パン）モード切替ボタン (どんなにズームしても画面右下に完全追従) */}
      <div style={btnStyle}>
        <button
          onClick={() => setIsMoveMode(!isMoveMode)}
          className={`p-4 rounded-full shadow-2xl border-2 flex items-center justify-center transition-all ${
            isMoveMode 
              ? 'bg-amber-400 text-amber-950 border-amber-300 shadow-[0_0_20px_rgba(251,191,36,0.8)] scale-110' 
              : 'bg-slate-800/90 text-slate-300 border-slate-500 backdrop-blur-md'
          }`}
          title="画面移動モード"
        >
          <Hand size={28} />
        </button>
      </div>

      {/* Main Canvas Container (Cropped) */}
      <main className="flex-none w-full flex items-center justify-center p-3 bg-slate-950 overflow-hidden" style={{ height: '45vh' }}>
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
          className="cursor-crosshair rounded-md shadow-[0_0_20px_rgba(0,0,0,0.5)] bg-slate-900 border border-slate-800"
          style={{ 
            width: 'auto',
            height: 'auto',
            maxWidth: '100%',
            maxHeight: '100%',
            aspectRatio: `${viewWidth} / ${viewHeight}`
          }}
        />
      </main>

      {/* Control Panel */}
      <div className="bg-slate-900 border-t border-slate-800 shrink-0 pb-safe flex flex-col flex-1 min-h-0">
        <div className="flex border-b border-slate-800 shrink-0">
          <button 
            className={`flex-1 py-3 text-xs font-bold tracking-wider ${activeTab === 'aim' ? 'text-teal-400 border-b-2 border-teal-400 bg-slate-800/50' : 'text-slate-500'}`}
            onClick={() => setActiveTab('aim')}
          >
            射出設定
          </button>
          <button 
            className={`flex-1 py-3 text-xs font-bold tracking-wider ${activeTab === 'walls' ? 'text-teal-400 border-b-2 border-teal-400 bg-slate-800/50' : 'text-slate-500'}`}
            onClick={() => setActiveTab('walls')}
          >
            壁範囲設定
          </button>
        </div>

        <div className="p-4 flex-1 overflow-y-auto">
          {activeTab === 'aim' && (
            <div className="space-y-4">
              <div className="flex items-center justify-between">
                <span className="text-xs text-slate-400">発射角度 (手動調整)</span>
                <div className="bg-slate-950 border border-slate-700 rounded px-3 py-1 font-mono text-sm">
                  {angle.toFixed(1)}°
                </div>
              </div>
              
              {/* Slider for coarse angle */}
              <input 
                type="range" 
                min="0" max="360" step="0.1" 
                value={angle} 
                onChange={(e) => setAngle(parseFloat(e.target.value))}
                className="w-full accent-teal-500"
              />

              {/* Fine tuning buttons */}
              <div className="flex gap-2">
                <button onClick={() => setAngle(a => (a - 1 + 360) % 360)} className="flex-1 bg-slate-800 py-2 rounded text-xs active:bg-slate-700">-1°</button>
                <button onClick={() => setAngle(a => (a - 0.1 + 360) % 360)} className="flex-1 bg-slate-800 py-2 rounded text-xs active:bg-slate-700">-0.1°</button>
                <button onClick={() => setAngle(a => (a + 0.1) % 360)} className="flex-1 bg-slate-800 py-2 rounded text-xs active:bg-slate-700">+0.1°</button>
                <button onClick={() => setAngle(a => (a + 1) % 360)} className="flex-1 bg-slate-800 py-2 rounded text-xs active:bg-slate-700">+1°</button>
              </div>

              {/* View Toggles */}
              <div className="flex gap-2">
                <button 
                  onClick={() => setShowBand(!showBand)} 
                  className={`flex-1 py-2 rounded text-xs font-medium border ${showBand ? 'bg-teal-500/20 text-teal-400 border-teal-500/50' : 'bg-slate-800 text-slate-400 border-slate-700'}`}
                >
                  幅 {showBand ? 'ON' : 'OFF'}
                </button>
                <button 
                  onClick={() => setShowReverseGuide(!showReverseGuide)} 
                  className={`flex-1 py-2 rounded text-xs font-medium border ${showReverseGuide ? 'bg-red-500/20 text-red-400 border-red-500/50' : 'bg-slate-800 text-slate-400 border-slate-700'}`}
                >
                  目安 {showReverseGuide ? 'ON' : 'OFF'}
                </button>
                <button 
                  onClick={() => setMaxBounces((b) => (b >= 10 ? 1 : b + 1))} 
                  className="flex-1 py-2 rounded text-xs font-medium border bg-slate-800 text-slate-200 border-slate-700"
                >
                  反射 {maxBounces}回
                </button>
                
                {/* Color Picker Button */}
                <button 
                  onClick={() => {
                    const colors = ['cyan', 'white', 'black'];
                    setLineColor(colors[(colors.indexOf(lineColor) + 1) % colors.length]);
                  }} 
                  className="flex-1 py-2 rounded text-xs font-medium border bg-slate-800 text-slate-200 border-slate-700 flex items-center justify-center gap-1"
                >
                  {lineColor === 'cyan' ? 'シアン' : lineColor === 'white' ? '白' : '黒'}
                  <div className={`w-2 h-2 rounded-full ${lineColor === 'cyan' ? 'bg-cyan-400' : lineColor === 'white' ? 'bg-white' : 'bg-black border border-slate-500'}`} />
                </button>
              </div>
            </div>
          )}

          {activeTab === 'walls' && (
            <div className="space-y-4">
              <div className="flex justify-between items-center mb-2">
                <span className="text-xs text-slate-400">壁の範囲設定 (%)</span>
                <div className="flex gap-2">
                  <button 
                    onClick={() => setShowWallLine(!showWallLine)}
                    className={`text-[10px] px-2 py-1 rounded border ${showWallLine ? 'bg-emerald-500/20 text-emerald-400 border-emerald-500/30' : 'bg-slate-800 text-slate-500 border-slate-700'}`}
                  >
                    枠線 {showWallLine ? 'ON' : 'OFF'}
                  </button>
                  <button 
                    onClick={() => setWallPercents(defaultWalls)}
                    className="flex items-center gap-1 text-[10px] text-slate-400 bg-slate-800 px-2 py-1 rounded border border-slate-700"
                  >
                    <RefreshCw size={10} /> リセット
                  </button>
                </div>
              </div>
              <div className="grid grid-cols-2 gap-x-4 gap-y-4">
                {['top', 'bottom', 'left', 'right'].map((dir) => (
                  <div key={dir} className="flex flex-col gap-1">
                    <div className="flex justify-between text-[10px]">
                      <span className="uppercase text-slate-500">{
                        dir === 'top' ? '上' : dir === 'bottom' ? '下' : dir === 'left' ? '左' : '右'
                      }</span>
                      <span className="text-slate-300">{wallPercents[dir]}%</span>
                    </div>
                    <input 
                      type="range" min="0" max="45" step="1"
                      value={wallPercents[dir]}
                      onChange={(e) => setWallPercents(p => ({...p, [dir]: parseInt(e.target.value)}))}
                      className="w-full accent-emerald-500 h-1 bg-slate-800 rounded-full appearance-none [&::-webkit-slider-thumb]:appearance-none [&::-webkit-slider-thumb]:w-3 [&::-webkit-slider-thumb]:h-3 [&::-webkit-slider-thumb]:bg-emerald-400 [&::-webkit-slider-thumb]:rounded-full"
                    />
                  </div>
                ))}
              </div>
            </div>
          )}
        </div>
      </div>
    </div>
  );
};

export default App;
