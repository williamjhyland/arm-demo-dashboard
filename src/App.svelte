<script>
    let selected = null;

    function pickObject(obj) {
        selected = obj;
        console.log(`Selected ${obj}`);
    }
</script>

<div class="dashboard">
    <div class="header">
        <h1>Viam Arm Demo Dashboard</h1>
        <div class="subtitle">Computer Vision & Robotic Control Interface</div>
    </div>
    
    <div class="content">
        <div class="camera-section">
            <div class="camera-container">
                <div class="camera-placeholder">
                    <div class="camera-icon">📹</div>
                    <div>
                        <div style="font-size: 1.1rem; font-weight: 600; margin-bottom: 0.5rem;">Camera Stream</div>
                        <div>Live feed will appear here</div>
                    </div>
                </div>
            </div>
            
            <div class="status-indicators">
                <div class="status-badge status-live">
                    <div class="status-dot"></div>
                    Camera Active
                </div>
                <div class="status-badge status-detection">
                    <div class="status-dot"></div>
                    Detection Ready
                </div>
            </div>
        </div>
        
        <div class="control-panel">
            <h2 class="panel-title">Object Selection</h2>
            
            <div class="object-buttons">
                <button class="object-btn btn-a" on:click={() => pickObject('A')}>
                    Pick Object A
                </button>
                <button class="object-btn btn-b" on:click={() => pickObject('B')}>
                    Pick Object B
                </button>
            </div>
            
            <div class="selection-display" class:has-selection={selected}>
                <div class="selection-label">Current Selection</div>
                <div class="selection-value" 
                     class:no-selection={!selected}
                     class:object-a={selected === 'A'}
                     class:object-b={selected === 'B'}>
                    {selected ? `Object ${selected}` : 'No object selected'}
                </div>
            </div>
        </div>
    </div>
</div>

<style>
    :global(body) {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background: #ffffff;
        min-height: 100vh;
        padding: 2rem;
        color: #000000;
        margin: 0;
    }

    .dashboard {
        max-width: 1200px;
        margin: 0 auto;
        background: #1a1a1a;
        border-radius: 12px;
        box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
        border: 1px solid #333;
        overflow: hidden;
    }

    .header {
        background: linear-gradient(135deg, #000000 0%, #1a1a1a 100%);
        color: white;
        padding: 2rem;
        text-align: center;
        position: relative;
        overflow: hidden;
        border-bottom: 2px solid #333;
    }

    .header::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: url("data:image/svg+xml,%3Csvg width='40' height='40' viewBox='0 0 40 40' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.05'%3E%3Cpath d='M20 20c0-5.5 4.5-10 10-10s10 4.5 10 10-4.5 10-10 10-10-4.5-10-10zm-10-10c0-5.5 4.5-10 10-10s10 4.5 10 10-4.5 10-10 10-10-4.5-10-10z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E") repeat;
        opacity: 1;
    }

    .header h1 {
        font-size: 2.5rem;
        font-weight: 700;
        margin-bottom: 0.5rem;
        position: relative;
        z-index: 1;
    }

    .header .subtitle {
        font-size: 1.1rem;
        opacity: 0.9;
        position: relative;
        z-index: 1;
    }

    .content {
        padding: 2.5rem;
        display: grid;
        grid-template-columns: 2fr 1fr;
        gap: 2.5rem;
        align-items: start;
        background: #1a1a1a;
    }

    .camera-section {
        display: flex;
        flex-direction: column;
    }

    .camera-container {
        position: relative;
        width: 100%;
        aspect-ratio: 16/9;
        background: #000000;
        border-radius: 8px;
        border: 2px solid #333;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow: hidden;
        box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.5);
        margin-bottom: 1.5rem;
    }

    .camera-placeholder {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1rem;
        color: #888;
        text-align: center;
    }

    .camera-icon {
        width: 60px;
        height: 60px;
        background: #333;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 24px;
        color: #fff;
    }

    .status-indicators {
        display: flex;
        gap: 1rem;
        justify-content: center;
        flex-wrap: wrap;
    }

    .status-badge {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        padding: 0.5rem 1rem;
        border-radius: 20px;
        font-size: 0.875rem;
        font-weight: 500;
    }

    .status-live {
        background: #1a4d3a;
        color: #4ade80;
        border: 1px solid #22c55e;
    }

    .status-detection {
        background: #1e1b00;
        color: #facc15;
        border: 1px solid #eab308;
    }

    .status-dot {
        width: 8px;
        height: 8px;
        border-radius: 50%;
        background: currentColor;
        animation: pulse 2s infinite;
    }

    @keyframes pulse {
        0%, 100% { opacity: 1; }
        50% { opacity: 0.5; }
    }

    .control-panel {
        background: #0a0a0a;
        border-radius: 8px;
        padding: 2rem;
        border: 2px solid #333;
    }

    .panel-title {
        font-size: 1.25rem;
        font-weight: 600;
        color: #ffffff;
        margin-bottom: 1.5rem;
        text-align: center;
    }

    .object-buttons {
        display: flex;
        flex-direction: column;
        gap: 1rem;
        margin-bottom: 2rem;
        align-items: center;
    }

    .object-btn {
        padding: 1rem 1.5rem;
        font-size: 1rem;
        font-weight: 600;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        transition: all 0.3s ease;
        position: relative;
        overflow: hidden;
        width: 200px;
        text-align: center;
    }

    .object-btn:before {
        content: '';
        position: absolute;
        top: 0;
        left: -100%;
        width: 100%;
        height: 100%;
        background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
        transition: left 0.5s;
    }

    .object-btn:hover:before {
        left: 100%;
    }

    .btn-a, .btn-b {
        background: linear-gradient(135deg, #ffffff 0%, #e5e5e5 100%);
        color: #000000;
        box-shadow: 0 4px 12px rgba(255, 255, 255, 0.2);
        border: 1px solid #ccc;
    }

    .btn-a:hover, .btn-b:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 16px rgba(255, 255, 255, 0.3);
        background: linear-gradient(135deg, #f5f5f5 0%, #d5d5d5 100%);
    }

    .btn-a:active, .btn-b:active {
        transform: translateY(0);
    }

    .selection-display {
        background: #000000;
        border-radius: 8px;
        padding: 1.5rem;
        text-align: center;
        border: 2px solid #333;
        transition: all 0.3s ease;
    }

    .selection-display.has-selection {
        border-color: #ffffff;
        box-shadow: 0 4px 12px rgba(255, 255, 255, 0.2);
    }

    .selection-label {
        font-size: 0.875rem;
        color: #888;
        margin-bottom: 0.5rem;
        font-weight: 500;
    }

    .selection-value {
        font-size: 1.5rem;
        font-weight: 700;
        color: #ffffff;
    }

    .selection-value.object-a {
        color: #ffffff;
    }

    .selection-value.object-b {
        color: #cccccc;
    }

    .no-selection {
        color: #666;
        font-style: italic;
    }

    @media (max-width: 768px) {
        .content {
            grid-template-columns: 1fr;
            gap: 2rem;
        }
        
        .header h1 {
            font-size: 2rem;
        }
        
        :global(body) {
            padding: 1rem;
        }
        
        .object-buttons {
            flex-direction: row;
        }
    }
</style>