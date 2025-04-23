 const SAFE_SETTINGS = {
        TARGET_FPS: 120000,             // Целевой FPS
        RENDER_SCALE: 1.0,          // Масштаб рендеринга (0.5-1)
        BLUR: 7,                    // Размытие (0-5)
        CONTRAST: 1.0,              // Контрастность
        BRIGHTNESS: 1.0,            // Яркость
        FRAME_SKIP: 5               // Пропуск кадров (1=off)
    };

    // Контроль совместимости
    const compatibilityCheck = () => {
        if (!HTMLCanvasElement.prototype.getContext) {
            console.error('[Optimizer] Canvas context not available');
            return false;
        }
        return true;
    };

    // Оптимизация канваса
    const safeCanvasOptimization = () => {
        try {
            const canvas = document.querySelector('canvas');
            if (!canvas) return;

            const ctx = canvas.getContext('2d');
            canvas.style.imageRendering = 'optimizeQuality';
            ctx.imageSmoothingEnabled = false;

            // Динамическое масштабирование
            const scale = SAFE_SETTINGS.RENDER_SCALE;
            canvas.width = canvas.width * scale;
            canvas.height = canvas.height * scale;
            canvas.style.transform = `scale(${1/scale})`;
        } catch (e) {
            console.error('[Optimizer] Canvas error:', e);
        }
    };

    // Оптимизированный RAF
    const stableFrameRate = () => {
        let last = 0;
        const callback = timestamp => {
            if (timestamp - last >= 1000/SAFE_SETTINGS.TARGET_FPS) {
                requestAnimationFrame(callback);
                last = timestamp;
            }
        };
        requestAnimationFrame(callback);
    };

    // Применение эффектов с защитой
    const applySafeEffects = () => {
        try {
            const container = document.getElementById('game-container') || document.body;
            container.style.filter = `
                blur(${SAFE_SETTINGS.BLUR}px)
                contrast(${SAFE_SETTINGS.CONTRAST})
                brightness(${SAFE_SETTINGS.BRIGHTNESS})
            `;
        } catch (e) {
            console.error('[Optimizer] Effect error:', e);
        }
    };

    // Инициализаци
    setTimeout(() => {
        if (!compatibilityCheck()) return;
        safeCanvasOptimization();
        stableFrameRate();
        applySafeEffects();
    }, 3000);
})();

//Играйте епта
