<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Umar AI — Создавай приложения и сайты с ИИ</title>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        /* ========== CSS Variables ========== */
        :root {
            --bg: #09090b;
            --bg-secondary: #0f0f13;
            --bg-card: #18181b;
            --bg-hover: #27272a;
            --bg-input: #1c1c21;
            --accent: #fbbf24;
            --accent-hover: #fcd34d;
            --accent-dim: rgba(251, 191, 36, 0.08);
            --accent-dim2: rgba(251, 191, 36, 0.15);
            --text: #fafafa;
            --text-secondary: #d4d4d8;
            --text-muted: #71717a;
            --border: #27272a;
            --border-light: #3f3f46;
            --error: #ef4444;
            --error-dim: rgba(239, 68, 68, 0.1);
            --success: #22c55e;
            --success-dim: rgba(34, 197, 94, 0.1);
            --warning: #f59e0b;
            --sidebar-w: 280px;
            --preview-w: 50%;
            --radius: 12px;
            --radius-sm: 8px;
            --radius-lg: 16px;
            --transition: 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            --shadow: 0 4px 24px rgba(0,0,0,0.4);
            --shadow-lg: 0 8px 40px rgba(0,0,0,0.6);
        }

        /* ========== Reset & Base ========== */
        *, *::before, *::after {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        html {
            font-size: 16px;
            scroll-behavior: smooth;
        }
        body {
            font-family: 'Space Grotesk', sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            overflow: hidden;
            -webkit-font-smoothing: antialiased;
        }
        ::selection {
            background: var(--accent-dim2);
            color: var(--accent);
        }
        a { color: var(--accent); text-decoration: none; }
        a:hover { text-decoration: underline; }
        button {
            font-family: inherit;
            cursor: pointer;
            border: none;
            outline: none;
            background: none;
            color: inherit;
            font-size: inherit;
        }
        input, textarea {
            font-family: inherit;
            border: none;
            outline: none;
            background: none;
            color: inherit;
            font-size: inherit;
        }
        img { max-width: 100%; display: block; }
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--border-light); }

        /* ========== Login Page ========== */
        .login-screen {
            position: fixed;
            inset: 0;
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
            background: var(--bg);
            overflow: hidden;
        }
        .login-screen.hidden { display: none; }
        .login-bg {
            position: absolute;
            inset: 0;
            overflow: hidden;
        }
        .login-bg-orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(120px);
            opacity: 0.3;
            animation: orbFloat 12s ease-in-out infinite alternate;
        }
        .login-bg-orb:nth-child(1) {
            width: 500px; height: 500px;
            background: var(--accent);
            top: -150px; left: -100px;
            animation-delay: 0s;
        }
        .login-bg-orb:nth-child(2) {
            width: 400px; height: 400px;
            background: #f97316;
            bottom: -100px; right: -100px;
            animation-delay: -4s;
        }
        .login-bg-orb:nth-child(3) {
            width: 300px; height: 300px;
            background: #eab308;
            top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            animation-delay: -8s;
            opacity: 0.15;
        }
        @keyframes orbFloat {
            0% { transform: translate(0, 0) scale(1); }
            33% { transform: translate(30px, -20px) scale(1.05); }
            66% { transform: translate(-20px, 30px) scale(0.95); }
            100% { transform: translate(10px, -10px) scale(1.02); }
        }
        .login-grid {
            position: absolute;
            inset: 0;
            background-image:
                linear-gradient(rgba(251,191,36,0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(251,191,36,0.03) 1px, transparent 1px);
            background-size: 60px 60px;
            mask-image: radial-gradient(ellipse at center, black 30%, transparent 70%);
        }
        .login-card {
            position: relative;
            z-index: 2;
            background: rgba(24, 24, 27, 0.8);
            backdrop-filter: blur(40px);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            padding: 48px 40px;
            width: 100%;
            max-width: 420px;
            text-align: center;
            box-shadow: var(--shadow-lg);
            animation: cardAppear 0.6s ease-out;
        }
        @keyframes cardAppear {
            from { opacity: 0; transform: translateY(20px) scale(0.96); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }
        .login-logo {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-bottom: 8px;
        }
        .login-logo-icon {
            width: 42px;
            height: 42px;
            background: linear-gradient(135deg, var(--accent), #f97316);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            color: #000;
            font-weight: 700;
            box-shadow: 0 0 24px rgba(251,191,36,0.3);
        }
        .login-logo-text {
            font-size: 28px;
            font-weight: 700;
            letter-spacing: -0.5px;
            background: linear-gradient(135deg, var(--text), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .login-subtitle {
            color: var(--text-muted);
            font-size: 14px;
            margin-bottom: 36px;
            line-height: 1.5;
        }
        .login-subtitle strong {
            color: var(--text-secondary);
        }
        .login-btn {
            width: 100%;
            padding: 14px 20px;
            border-radius: var(--radius);
            font-size: 15px;
            font-weight: 500;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            transition: var(--transition);
            margin-bottom: 12px;
            position: relative;
            overflow: hidden;
        }
        .login-btn::after {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(rgba(255,255,255,0.05), transparent);
            opacity: 0;
            transition: var(--transition);
        }
        .login-btn:hover::after { opacity: 1; }
        .login-btn-google {
            background: #fff;
            color: #1a1a1a;
            border: 1px solid #e5e5e5;
        }
        .login-btn-google:hover {
            background: #f5f5f5;
            border-color: #d4d4d4;
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        .login-btn-apple {
            background: #fff;
            color: #1a1a1a;
            border: 1px solid #e5e5e5;
        }
        .login-btn-apple:hover {
            background: #f5f5f5;
            border-color: #d4d4d4;
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        .login-btn-icon {
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
        }
        .login-divider {
            display: flex;
            align-items: center;
            gap: 16px;
            margin: 24px 0;
            color: var(--text-muted);
            font-size: 13px;
        }
        .login-divider::before,
        .login-divider::after {
            content: '';
            flex: 1;
            height: 1px;
            background: var(--border);
        }
        .login-terms {
            font-size: 12px;
            color: var(--text-muted);
            line-height: 1.6;
            margin-top: 8px;
        }
        .login-terms a { color: var(--text-secondary); }
        .login-terms a:hover { color: var(--accent); text-decoration: underline; }

        /* ========== Auth Modals ========== */
        .auth-modal-overlay {
            position: fixed;
            inset: 0;
            z-index: 1100;
            background: rgba(0,0,0,0.7);
            backdrop-filter: blur(8px);
            display: flex;
            align-items: center;
            justify-content: center;
            animation: fadeIn 0.2s ease;
        }
        .auth-modal-overlay.hidden { display: none; }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .auth-modal {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            padding: 32px;
            width: 100%;
            max-width: 400px;
            box-shadow: var(--shadow-lg);
            animation: modalSlideIn 0.3s ease;
        }
        @keyframes modalSlideIn {
            from { opacity: 0; transform: translateY(16px) scale(0.96); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }
        .auth-modal-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 24px;
        }
        .auth-modal-title {
            font-size: 18px;
            font-weight: 600;
        }
        .auth-modal-close {
            width: 32px;
            height: 32px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            transition: var(--transition);
        }
        .auth-modal-close:hover {
            background: var(--bg-hover);
            color: var(--text);
        }
        .auth-account {
            display: flex;
            align-items: center;
            gap: 14px;
            padding: 14px 16px;
            border-radius: var(--radius);
            border: 1px solid var(--border);
            cursor: pointer;
            transition: var(--transition);
            margin-bottom: 10px;
        }
        .auth-account:hover {
            background: var(--bg-hover);
            border-color: var(--border-light);
        }
        .auth-account-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            font-weight: 600;
            color: #fff;
            flex-shrink: 0;
        }
        .auth-account-info { text-align: left; }
        .auth-account-name {
            font-size: 14px;
            font-weight: 500;
            color: var(--text);
        }
        .auth-account-email {
            font-size: 12px;
            color: var(--text-muted);
            margin-top: 2px;
        }

        /* ========== Main App Layout ========== */
        .main-app {
            display: flex;
            height: 100vh;
            width: 100vw;
        }
        .main-app.hidden { display: none; }

        /* ========== Sidebar ========== */
        .sidebar {
            width: var(--sidebar-w);
            min-width: var(--sidebar-w);
            height: 100vh;
            background: var(--bg-secondary);
            border-right: 1px solid var(--border);
            display: flex;
            flex-direction: column;
            transition: var(--transition);
            position: relative;
            z-index: 100;
        }
        .sidebar.collapsed {
            width: 0;
            min-width: 0;
            overflow: hidden;
            border-right: none;
        }
        .sidebar-header {
            padding: 16px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid var(--border);
            min-height: 64px;
        }
        .sidebar-logo {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .sidebar-logo-icon {
            width: 32px;
            height: 32px;
            background: linear-gradient(135deg, var(--accent), #f97316);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            color: #000;
            font-weight: 700;
        }
        .sidebar-logo-text {
            font-size: 18px;
            font-weight: 700;
            letter-spacing: -0.3px;
        }
        .sidebar-toggle {
            width: 32px;
            height: 32px;
            border-radius: var(--radius-sm);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            transition: var(--transition);
        }
        .sidebar-toggle:hover {
            background: var(--bg-hover);
            color: var(--text);
        }
        .sidebar-new-chat {
            margin: 12px 16px;
            padding: 12px 16px;
            border-radius: var(--radius);
            border: 1px dashed var(--border-light);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            font-size: 14px;
            font-weight: 500;
            color: var(--text-secondary);
            transition: var(--transition);
        }
        .sidebar-new-chat:hover {
            background: var(--accent-dim);
            border-color: var(--accent);
            color: var(--accent);
        }
        .sidebar-section-title {
            padding: 8px 16px 4px;
            font-size: 11px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.8px;
            color: var(--text-muted);
        }
        .sidebar-history {
            flex: 1;
            overflow-y: auto;
            padding: 4px 8px;
        }
        .history-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px 12px;
            border-radius: var(--radius-sm);
            cursor: pointer;
            transition: var(--transition);
            margin-bottom: 2px;
            position: relative;
        }
        .history-item:hover {
            background: var(--bg-hover);
        }
        .history-item.active {
            background: var(--accent-dim);
        }
        .history-item-icon {
            width: 18px;
            color: var(--text-muted);
            font-size: 13px;
            flex-shrink: 0;
        }
        .history-item-text {
            font-size: 13px;
            color: var(--text-secondary);
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            flex: 1;
        }
        .history-item.active .history-item-text { color: var(--accent); }
        .history-item-delete {
            width: 24px;
            height: 24px;
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            opacity: 0;
            transition: var(--transition);
            flex-shrink: 0;
            font-size: 11px;
        }
        .history-item:hover .history-item-delete { opacity: 1; }
        .history-item-delete:hover {
            background: var(--error-dim);
            color: var(--error);
        }
        .sidebar-footer {
            border-top: 1px solid var(--border);
            padding: 12px;
        }
        .sidebar-model-select {
            width: 100%;
            padding: 10px 12px;
            border-radius: var(--radius-sm);
            background: var(--bg-card);
            border: 1px solid var(--border);
            color: var(--text);
            font-size: 13px;
            font-family: inherit;
            cursor: pointer;
            transition: var(--transition);
            appearance: none;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%2371717a' stroke-width='2'%3E%3Cpath d='M6 9l6 6 6-6'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: right 12px center;
            padding-right: 32px;
        }
        .sidebar-model-select:hover { border-color: var(--border-light); }
        .sidebar-model-select:focus { border-color: var(--accent); }
        .sidebar-model-select option {
            background: var(--bg-card);
            color: var(--text);
            padding: 8px;
        }
        .sidebar-profile {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px 12px;
            border-radius: var(--radius-sm);
            cursor: pointer;
            transition: var(--transition);
            margin-top: 8px;
        }
        .sidebar-profile:hover { background: var(--bg-hover); }
        .sidebar-profile-avatar {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 13px;
            font-weight: 600;
            color: #fff;
            flex-shrink: 0;
        }
        .sidebar-profile-name {
            font-size: 13px;
            font-weight: 500;
            flex: 1;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .sidebar-logout {
            width: 28px;
            height: 28px;
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            transition: var(--transition);
            font-size: 13px;
        }
        .sidebar-logout:hover {
            background: var(--error-dim);
            color: var(--error);
        }

        /* ========== Chat Area ========== */
        .chat-container {
            flex: 1;
            display: flex;
            flex-direction: column;
            height: 100vh;
            min-width: 0;
            position: relative;
        }
        .chat-header {
            padding: 12px 20px;
            border-bottom: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            min-height: 56px;
            background: rgba(9,9,11,0.8);
            backdrop-filter: blur(12px);
        }
        .chat-header-left {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .chat-header-sidebar-toggle {
            width: 32px;
            height: 32px;
            border-radius: var(--radius-sm);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            transition: var(--transition);
        }
        .chat-header-sidebar-toggle:hover {
            background: var(--bg-hover);
            color: var(--text);
        }
        .chat-header-title {
            font-size: 14px;
            font-weight: 500;
            color: var(--text-secondary);
        }
        .chat-header-actions {
            display: flex;
            align-items: center;
            gap: 4px;
        }
        .chat-header-btn {
            width: 36px;
            height: 36px;
            border-radius: var(--radius-sm);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            transition: var(--transition);
            font-size: 14px;
        }
        .chat-header-btn:hover {
            background: var(--bg-hover);
            color: var(--text);
        }
        .chat-header-btn.active {
            background: var(--accent-dim);
            color: var(--accent);
        }
        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 24px 0;
        }
        .chat-welcome {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100%;
            padding: 40px 20px;
            text-align: center;
        }
        .chat-welcome-icon {
            width: 72px;
            height: 72px;
            background: linear-gradient(135deg, var(--accent), #f97316);
            border-radius: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            color: #000;
            font-weight: 700;
            margin-bottom: 24px;
            box-shadow: 0 0 48px rgba(251,191,36,0.2);
            animation: welcomePulse 3s ease-in-out infinite;
        }
        @keyframes welcomePulse {
            0%, 100% { box-shadow: 0 0 48px rgba(251,191,36,0.2); }
            50% { box-shadow: 0 0 64px rgba(251,191,36,0.35); }
        }
        .chat-welcome h2 {
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 8px;
            letter-spacing: -0.5px;
        }
        .chat-welcome p {
            font-size: 15px;
            color: var(--text-muted);
            max-width: 500px;
            line-height: 1.6;
            margin-bottom: 32px;
        }
        .chat-welcome-suggestions {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            max-width: 560px;
            width: 100%;
        }
        .suggestion-card {
            padding: 16px;
            border-radius: var(--radius);
            border: 1px solid var(--border);
            background: var(--bg-card);
            text-align: left;
            cursor: pointer;
            transition: var(--transition);
        }
        .suggestion-card:hover {
            border-color: var(--accent);
            background: var(--accent-dim);
            transform: translateY(-2px);
        }
        .suggestion-card-icon {
            font-size: 18px;
            margin-bottom: 8px;
            color: var(--accent);
        }
        .suggestion-card-text {
            font-size: 13px;
            color: var(--text-secondary);
            line-height: 1.4;
        }

        /* ========== Messages ========== */
        .message {
            padding: 16px 24px;
            animation: msgAppear 0.3s ease;
        }
        @keyframes msgAppear {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .message-user {
            display: flex;
            justify-content: flex-end;
        }
        .message-user-bubble {
            background: var(--accent);
            color: #000;
            padding: 12px 18px;
            border-radius: 18px 18px 4px 18px;
            max-width: 70%;
            font-size: 14px;
            font-weight: 500;
            line-height: 1.5;
            word-break: break-word;
        }
        .message-ai {
            display: flex;
            gap: 14px;
            max-width: 900px;
            margin: 0 auto;
        }
        .message-ai-avatar {
            width: 32px;
            height: 32px;
            border-radius: 10px;
            background: linear-gradient(135deg, var(--accent), #f97316);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            color: #000;
            font-weight: 700;
            flex-shrink: 0;
            margin-top: 2px;
        }
        .message-ai-content {
            flex: 1;
            min-width: 0;
        }
        .message-ai-text {
            font-size: 14px;
            line-height: 1.7;
            color: var(--text-secondary);
        }
        .message-ai-text p { margin-bottom: 12px; }
        .message-ai-text p:last-child { margin-bottom: 0; }
        .message-ai-text strong { color: var(--text); font-weight: 600; }
        .message-ai-text ul, .message-ai-text ol {
            margin: 8px 0;
            padding-left: 24px;
        }
        .message-ai-text li {
            margin-bottom: 4px;
            color: var(--text-secondary);
        }
        .message-plan {
            background: var(--accent-dim);
            border: 1px solid rgba(251,191,36,0.15);
            border-radius: var(--radius);
            padding: 16px;
            margin-bottom: 16px;
        }
        .message-plan-title {
            font-size: 12px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.8px;
            color: var(--accent);
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .message-plan-items {
            list-style: none;
            padding: 0;
        }
        .message-plan-items li {
            font-size: 13px;
            color: var(--text-secondary);
            padding: 4px 0;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .message-plan-items li i {
            color: var(--accent);
            font-size: 11px;
        }
        .message-build-title {
            font-size: 12px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.8px;
            color: var(--success);
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .message-actions {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-top: 16px;
            flex-wrap: wrap;
        }
        .msg-action-btn {
            padding: 8px 14px;
            border-radius: var(--radius-sm);
            border: 1px solid var(--border);
            font-size: 12px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 6px;
            color: var(--text-secondary);
            transition: var(--transition);
        }
        .msg-action-btn:hover {
            background: var(--bg-hover);
            border-color: var(--border-light);
            color: var(--text);
        }
        .msg-action-btn.primary {
            background: var(--accent);
            color: #000;
            border-color: var(--accent);
            font-weight: 600;
        }
        .msg-action-btn.primary:hover {
            background: var(--accent-hover);
        }
        .msg-action-btn i { font-size: 12px; }

        /* ========== Thinking Dots ========== */
        .thinking-indicator {
            display: flex;
            align-items: center;
            gap: 14px;
            padding: 16px 24px;
            animation: msgAppear 0.3s ease;
        }
        .thinking-dots {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        .thinking-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--accent);
            animation: dotBounce 1.2s ease-in-out infinite;
        }
        .thinking-dot:nth-child(1) { animation-delay: 0s; }
        .thinking-dot:nth-child(2) { animation-delay: 0.15s; }
        .thinking-dot:nth-child(3) { animation-delay: 0.3s; }
        @keyframes dotBounce {
            0%, 80%, 100% { transform: translateY(0); opacity: 0.4; }
            40% { transform: translateY(-10px); opacity: 1; }
        }
        .thinking-label {
            font-size: 13px;
            color: var(--text-muted);
        }

        /* ========== Code Blocks ========== */
        .code-block-wrapper {
            margin: 12px 0;
            border-radius: var(--radius);
            border: 1px solid var(--border);
            overflow: hidden;
            background: #0d0d12;
        }
        .code-block-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px 16px;
            background: rgba(255,255,255,0.03);
            border-bottom: 1px solid var(--border);
        }
        .code-block-lang {
            font-size: 12px;
            font-weight: 500;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        .code-block-copy {
            padding: 4px 10px;
            border-radius: 6px;
            font-size: 11px;
            color: var(--text-muted);
            display: flex;
            align-items: center;
            gap: 4px;
            transition: var(--transition);
        }
        .code-block-copy:hover {
            background: var(--bg-hover);
            color: var(--text);
        }
        .code-block-copy.copied {
            color: var(--success);
        }
        .code-block {
            padding: 16px;
            overflow-x: auto;
            font-family: 'JetBrains Mono', monospace;
            font-size: 13px;
            line-height: 1.6;
            color: #c9d1d9;
            tab-size: 2;
        }
        .code-block .kw { color: #ff7b72; }
        .code-block .str { color: #a5d6ff; }
        .code-block .cm { color: #8b949e; }
        .code-block .fn { color: #d2a8ff; }
        .code-block .num { color: #79c0ff; }
        .code-block .tag { color: #7ee787; }
        .code-block .attr { color: #79c0ff; }
        .code-block .val { color: #a5d6ff; }

        /* ========== File Preview in Chat ========== */
        .chat-file-preview {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 8px 12px;
            border-radius: var(--radius-sm);
            background: var(--bg-card);
            border: 1px solid var(--border);
            margin-bottom: 8px;
            font-size: 13px;
            color: var(--text-secondary);
            max-width: 300px;
        }
        .chat-file-preview i { color: var(--accent); }
        .chat-file-preview-name {
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .chat-image-preview {
            max-width: 240px;
            border-radius: var(--radius);
            border: 1px solid var(--border);
            margin-bottom: 8px;
        }

        /* ========== Input Area ========== */
        .chat-input-area {
            padding: 16px 24px 20px;
            border-top: 1px solid var(--border);
            background: rgba(9,9,11,0.9);
            backdrop-filter: blur(12px);
        }
        .chat-input-wrapper {
            max-width: 860px;
            margin: 0 auto;
        }
        .chat-input-container {
            display: flex;
            align-items: flex-end;
            gap: 10px;
            background: var(--bg-input);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            padding: 8px 8px 8px 16px;
            transition: var(--transition);
        }
        .chat-input-container:focus-within {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-dim);
        }
        .chat-input-left {
            display: flex;
            align-items: center;
            gap: 4px;
        }
        .chat-input-file-btn {
            width: 34px;
            height: 34px;
            border-radius: var(--radius-sm);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            transition: var(--transition);
            font-size: 15px;
        }
        .chat-input-file-btn:hover {
            background: var(--bg-hover);
            color: var(--text);
        }
        .chat-input {
            flex: 1;
            resize: none;
            min-height: 24px;
            max-height: 160px;
            padding: 6px 0;
            font-size: 14px;
            line-height: 1.5;
            color: var(--text);
            background: transparent;
        }
        .chat-input::placeholder { color: var(--text-muted); }
        .chat-send-btn {
            width: 38px;
            height: 38px;
            border-radius: var(--radius);
            background: var(--accent);
            color: #000;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 15px;
            transition: var(--transition);
            flex-shrink: 0;
        }
        .chat-send-btn:hover {
            background: var(--accent-hover);
            transform: scale(1.05);
        }
        .chat-send-btn:disabled {
            opacity: 0.3;
            cursor: not-allowed;
            transform: none;
        }
        .chat-input-hint {
            text-align: center;
            font-size: 11px;
            color: var(--text-muted);
            margin-top: 8px;
            opacity: 0.7;
        }
        .chat-files-preview {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 8px;
        }
        .chat-file-chip {
            display: flex;
            align-items: center;
            gap: 6px;
            padding: 6px 10px;
            border-radius: var(--radius-sm);
            background: var(--bg-card);
            border: 1px solid var(--border);
            font-size: 12px;
            color: var(--text-secondary);
            animation: chipAppear 0.2s ease;
        }
        @keyframes chipAppear {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
        }
        .chat-file-chip-remove {
            width: 18px;
            height: 18px;
            border-radius: 4px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            font-size: 10px;
            transition: var(--transition);
        }
        .chat-file-chip-remove:hover {
            background: var(--error-dim);
            color: var(--error);
        }
        .chat-file-chip img {
            width: 28px;
            height: 28px;
            border-radius: 4px;
            object-fit: cover;
        }

        /* ========== Preview Panel ========== */
        .preview-panel {
            width: 0;
            min-width: 0;
            height: 100vh;
            border-left: 1px solid var(--border);
            background: var(--bg-secondary);
            display: flex;
            flex-direction: column;
            overflow: hidden;
            transition: width 0.3s ease, min-width 0.3s ease;
        }
        .preview-panel.open {
            width: var(--preview-w);
            min-width: var(--preview-w);
        }
        .preview-header {
            padding: 12px 16px;
            border-bottom: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            min-height: 56px;
        }
        .preview-title {
            font-size: 14px;
            font-weight: 500;
            color: var(--text-secondary);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .preview-title-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--success);
            animation: livePulse 2s ease-in-out infinite;
        }
        @keyframes livePulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.4; }
        }
        .preview-url {
            padding: 8px 12px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm);
            font-size: 12px;
            color: var(--text-muted);
            font-family: 'JetBrains Mono', monospace;
            display: flex;
            align-items: center;
            gap: 8px;
            flex: 1;
            margin: 0 12px;
            max-width: 400px;
            overflow: hidden;
        }
        .preview-url-text {
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .preview-close {
            width: 32px;
            height: 32px;
            border-radius: var(--radius-sm);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            transition: var(--transition);
        }
        .preview-close:hover {
            background: var(--bg-hover);
            color: var(--text);
        }
        .preview-frame {
            flex: 1;
            background: #fff;
            border: none;
            width: 100%;
        }

        /* ========== Publish Modal ========== */
        .modal-overlay {
            position: fixed;
            inset: 0;
            z-index: 200;
            background: rgba(0,0,0,0.7);
            backdrop-filter: blur(8px);
            display: flex;
            align-items: center;
            justify-content: center;
            animation: fadeIn 0.2s ease;
        }
        .modal-overlay.hidden { display: none; }
        .modal {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            width: 100%;
            max-width: 480px;
            box-shadow: var(--shadow-lg);
            animation: modalSlideIn 0.3s ease;
            overflow: hidden;
        }
        .modal-header {
            padding: 24px 24px 0;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        .modal-title {
            font-size: 20px;
            font-weight: 700;
        }
        .modal-close {
            width: 32px;
            height: 32px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            transition: var(--transition);
        }
        .modal-close:hover {
            background: var(--bg-hover);
            color: var(--text);
        }
        .modal-body { padding: 24px; }
        .modal-footer {
            padding: 16px 24px;
            border-top: 1px solid var(--border);
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }
        .modal-btn {
            padding: 10px 20px;
            border-radius: var(--radius);
            font-size: 14px;
            font-weight: 500;
            transition: var(--transition);
        }
        .modal-btn-secondary {
            background: var(--bg-hover);
            color: var(--text-secondary);
        }
        .modal-btn-secondary:hover {
            background: var(--border);
            color: var(--text);
        }
        .modal-btn-primary {
            background: var(--accent);
            color: #000;
            font-weight: 600;
        }
        .modal-btn-primary:hover {
            background: var(--accent-hover);
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-label {
            display: block;
            font-size: 13px;
            font-weight: 500;
            color: var(--text-secondary);
            margin-bottom: 6px;
        }
        .form-hint {
            font-size: 12px;
            color: var(--text-muted);
            margin-top: 4px;
        }
        .form-input {
            width: 100%;
            padding: 10px 14px;
            border-radius: var(--radius-sm);
            background: var(--bg-input);
            border: 1px solid var(--border);
            color: var(--text);
            font-size: 14px;
            font-family: inherit;
            transition: var(--transition);
        }
        .form-input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-dim);
        }
        .form-input-prefix {
            display: flex;
            align-items: center;
            gap: 0;
        }
        .form-input-prefix span {
            padding: 10px 12px;
            background: var(--bg-hover);
            border: 1px solid var(--border);
            border-right: none;
            border-radius: var(--radius-sm) 0 0 var(--radius-sm);
            font-size: 13px;
            color: var(--text-muted);
            font-family: 'JetBrains Mono', monospace;
            white-space: nowrap;
        }
        .form-input-prefix input {
            border-radius: 0 var(--radius-sm) var(--radius-sm) 0;
        }
        .publish-success {
            text-align: center;
            padding: 20px 0;
        }
        .publish-success-icon {
            width: 56px;
            height: 56px;
            border-radius: 50%;
            background: var(--success-dim);
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 16px;
            font-size: 24px;
            color: var(--success);
        }
        .publish-success-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 8px;
        }
        .publish-success-link {
            padding: 10px 16px;
            background: var(--bg-hover);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm);
            font-family: 'JetBrains Mono', monospace;
            font-size: 13px;
            color: var(--accent);
            word-break: break-all;
            margin: 12px 0;
            cursor: pointer;
            transition: var(--transition);
        }
        .publish-success-link:hover {
            background: var(--accent-dim);
            border-color: var(--accent);
        }

        /* ========== Profile Modal ========== */
        .profile-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }
        .profile-avatar-large {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            font-weight: 700;
            color: #fff;
            margin-bottom: 16px;
            position: relative;
        }
        .profile-avatar-large::after {
            content: '';
            position: absolute;
            inset: -3px;
            border-radius: 50%;
            border: 2px solid var(--accent);
            opacity: 0.5;
        }
        .profile-name {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 4px;
        }
        .profile-email {
            font-size: 14px;
            color: var(--text-muted);
            margin-bottom: 24px;
        }
        .profile-stats {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 12px;
            width: 100%;
            margin-bottom: 24px;
        }
        .profile-stat {
            padding: 16px;
            background: var(--bg-hover);
            border-radius: var(--radius);
        }
        .profile-stat-value {
            font-size: 22px;
            font-weight: 700;
            color: var(--accent);
        }
        .profile-stat-label {
            font-size: 11px;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-top: 2px;
        }
        .profile-plan-badge {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            padding: 6px 14px;
            border-radius: 20px;
            background: var(--accent-dim);
            border: 1px solid rgba(251,191,36,0.2);
            font-size: 13px;
            font-weight: 600;
            color: var(--accent);
            margin-bottom: 20px;
        }

        /* ========== Toast Notifications ========== */
        .toast-container {
            position: fixed;
            bottom: 24px;
            right: 24px;
            z-index: 9999;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        .toast {
            padding: 12px 20px;
            border-radius: var(--radius);
            background: var(--bg-card);
            border: 1px solid var(--border);
            box-shadow: var(--shadow);
            font-size: 13px;
            color: var(--text-secondary);
            display: flex;
            align-items: center;
            gap: 10px;
            animation: toastIn 0.3s ease;
            max-width: 360px;
        }
        .toast.toast-out {
            animation: toastOut 0.3s ease forwards;
        }
        @keyframes toastIn {
            from { opacity: 0; transform: translateX(20px); }
            to { opacity: 1; transform: translateX(0); }
        }
        @keyframes toastOut {
            from { opacity: 1; transform: translateX(0); }
            to { opacity: 0; transform: translateX(20px); }
        }
        .toast-success i { color: var(--success); }
        .toast-error i { color: var(--error); }
        .toast-info i { color: var(--accent); }

        /* ========== Mobile Sidebar Overlay ========== */
        .sidebar-overlay {
            position: fixed;
            inset: 0;
            z-index: 90;
            background: rgba(0,0,0,0.5);
            display: none;
        }
        .sidebar-overlay.active { display: block; }

        /* ========== Responsive ========== */
        @media (max-width: 768px) {
            .sidebar {
                position: fixed;
                left: 0;
                top: 0;
                z-index: 100;
                box-shadow: var(--shadow-lg);
            }
            .sidebar.collapsed {
                transform: translateX(-100%);
            }
            .preview-panel.open {
                position: fixed;
                right: 0;
                top: 0;
                z-index: 100;
                width: 100%;
                min-width: 100%;
            }
            .chat-welcome-suggestions {
                grid-template-columns: 1fr;
            }
            .chat-messages { padding: 16px 0; }
            .message { padding: 12px 16px; }
            .message-ai { flex-direction: column; gap: 8px; }
            .message-user-bubble { max-width: 85%; }
            .chat-input-area { padding: 12px 16px 16px; }
        }

        /* ========== Utility ========== */
        .hidden { display: none !important; }
        .truncate { white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .sr-only {
            position: absolute;
            width: 1px;
            height: 1px;
            padding: 0;
            margin: -1px;
            overflow: hidden;
            clip: rect(0,0,0,0);
            white-space: nowrap;
            border: 0;
        }

        /* ========== Streaming text cursor ========== */
        .streaming-cursor::after {
            content: '|';
            animation: cursorBlink 0.8s step-end infinite;
            color: var(--accent);
            margin-left: 1px;
        }
        @keyframes cursorBlink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }

        /* ========== Plan/Build phase badges ========== */
        .phase-badge {
            display: inline-flex;
            align-items: center;
            gap: 5px;
            padding: 3px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        .phase-plan {
            background: var(--accent-dim);
            color: var(--accent);
            border: 1px solid rgba(251,191,36,0.2);
        }
        .phase-build {
            background: var(--success-dim);
            color: var(--success);
            border: 1px solid rgba(34,197,94,0.2);
        }

        /* ========== Loading bar for generation ========== */
        .gen-progress {
            height: 2px;
            background: var(--border);
            border-radius: 1px;
            overflow: hidden;
            margin: 12px 0;
        }
        .gen-progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--accent), #f97316);
            border-radius: 1px;
            width: 0%;
            transition: width 0.3s ease;
        }

        /* ========== Drag and drop overlay ========== */
        .drop-overlay {
            position: fixed;
            inset: 0;
            z-index: 500;
            background: rgba(9,9,11,0.9);
            border: 3px dashed var(--accent);
            display: flex;
            align-items: center;
            justify-content: center;
            animation: fadeIn 0.2s ease;
        }
        .drop-overlay.hidden { display: none; }
        .drop-overlay-content {
            text-align: center;
        }
        .drop-overlay-icon {
            font-size: 48px;
            color: var(--accent);
            margin-bottom: 16px;
        }
        .drop-overlay-text {
            font-size: 18px;
            font-weight: 600;
            color: var(--text);
            margin-bottom: 8px;
        }
        .drop-overlay-hint {
            font-size: 14px;
            color: var(--text-muted);
        }
    </style>
</head>
<body>

    <!-- ========== Drag & Drop Overlay ========== -->
    <div class="drop-overlay hidden" id="dropOverlay">
        <div class="drop-overlay-content">
            <div class="drop-overlay-icon"><i class="fas fa-cloud-upload-alt"></i></div>
            <div class="drop-overlay-text">Перетащите файлы сюда</div>
            <div class="drop-overlay-hint">Фото, документы, код — любой формат</div>
        </div>
    </div>

    <!-- ========== Login Screen ========== -->
    <div class="login-screen" id="loginScreen">
        <div class="login-bg">
            <div class="login-bg-orb"></div>
            <div class="login-bg-orb"></div>
            <div class="login-bg-orb"></div>
            <div class="login-grid"></div>
        </div>
        <div class="login-card">
            <div class="login-logo">
                <div class="login-logo-icon">U</div>
                <span class="login-logo-text">Umar AI</span>
            </div>
            <p class="login-subtitle">
                Создавай приложения и сайты с ИИ.<br>
                <strong>Полностью бесплатно. Без лимитов.</strong>
            </p>
            <button class="login-btn login-btn-google" onclick="showGoogleAuth()">
                <span class="login-btn-icon"><svg width="18" height="18" viewBox="0 0 24 24"><path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92a5.06 5.06 0 01-2.2 3.32v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.1z" fill="#4285F4"/><path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/><path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/><path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/></svg></span>
                Continue with Google
            </button>
            <button class="login-btn login-btn-apple" onclick="showAppleAuth()">
                <span class="login-btn-icon"><i class="fab fa-apple" style="font-size:20px"></i></span>
                Continue with Apple
            </button>
            <div class="login-divider">TO CONTINUE TO UMARAI</div>
            <p class="login-terms">
                Нажимая кнопку, вы соглашаетесь с<br>
                <a href="#">Условиями использования</a> и <a href="#">Политикой конфиденциальности</a>
            </p>
        </div>
    </div>

    <!-- ========== Google Auth Modal ========== -->
    <div class="auth-modal-overlay hidden" id="googleAuthModal">
        <div class="auth-modal">
            <div class="auth-modal-header">
                <span class="auth-modal-title">Войти с Google</span>
                <button class="auth-modal-close" onclick="closeAuthModals()"><i class="fas fa-times"></i></button>
            </div>
            <div id="googleAccounts"></div>
        </div>
    </div>

    <!-- ========== Apple Auth Modal ========== -->
    <div class="auth-modal-overlay hidden" id="appleAuthModal">
        <div class="auth-modal">
            <div class="auth-modal-header">
                <span class="auth-modal-title">Войти с Apple</span>
                <button class="auth-modal-close" onclick="closeAuthModals()"><i class="fas fa-times"></i></button>
            </div>
            <div id="appleAccounts"></div>
        </div>
    </div>

    <!-- ========== Main App ========== -->
    <div class="main-app hidden" id="mainApp">
        <!-- Sidebar Overlay (mobile) -->
        <div class="sidebar-overlay" id="sidebarOverlay" onclick="toggleSidebar()"></div>

        <!-- Sidebar -->
        <aside class="sidebar" id="sidebar">
            <div class="sidebar-header">
                <div class="sidebar-logo">
                    <div class="sidebar-logo-icon">U</div>
                    <span class="sidebar-logo-text">Umar AI</span>
                </div>
                <button class="sidebar-toggle" onclick="toggleSidebar()" aria-label="Свернуть боковую панель">
                    <i class="fas fa-chevron-left"></i>
                </button>
            </div>
            <button class="sidebar-new-chat" onclick="newChat()">
                <i class="fas fa-plus"></i>
                Новый чат
            </button>
            <div class="sidebar-section-title">История</div>
            <div class="sidebar-history" id="chatHistory"></div>
            <div class="sidebar-footer">
                <select class="sidebar-model-select" id="modelSelect" aria-label="Выбрать модель ИИ">
                    <optgroup label="OpenAI">
                        <option value="gpt-5.4" selected>OpenAI GPT-5.4</option>
                        <option value="gpt-5.3">OpenAI GPT-5.3</option>
                        <option value="gpt-5.2">OpenAI GPT-5.2</option>
                        <option value="gpt-5.1">OpenAI GPT-5.1</option>
                    </optgroup>
                    <optgroup label="Anthropic Claude">
                        <option value="claude-4-opus">Claude 4 Opus</option>
                        <option value="claude-4-sonnet">Claude 4 Sonnet</option>
                        <option value="claude-4-haiku">Claude 4 Haiku</option>
                        <option value="claude-3.5-sonnet">Claude 3.5 Sonnet</option>
                        <option value="claude-3.5-haiku">Claude 3.5 Haiku</option>
                        <option value="claude-3-opus">Claude 3 Opus</option>
                        <option value="claude-3-sonnet">Claude 3 Sonnet</option>
                    </optgroup>
                    <optgroup label="Google">
                        <option value="gemini-3-pro">Gemini 3 Pro</option>
                        <option value="gemini-3.1-pro">Gemini 3.1 Pro</option>
                    </optgroup>
                    <optgroup label="Другие">
                        <option value="grok-4">Grok 4</option>
                        <option value="qwem-3-max">Qwem 3 Max</option>
                        <option value="kimi-k2">DeepInfra Kimi K2</option>
                        <option value="deepseek-v3">DeepSeek V3</option>
                        <option value="llama-3.3">Llama 3.3 70B</option>
                    </optgroup>
                </select>
                <div class="sidebar-profile" onclick="openProfile()">
                    <div class="sidebar-profile-avatar" id="sidebarAvatar">U</div>
                    <span class="sidebar-profile-name" id="sidebarName">User</span>
                    <button class="sidebar-logout" onclick="event.stopPropagation();logout()" aria-label="Выйти из аккаунта">
                        <i class="fas fa-sign-out-alt"></i>
                    </button>
                </div>
            </div>
        </aside>

        <!-- Chat Container -->
        <div class="chat-container">
            <header class="chat-header">
                <div class="chat-header-left">
                    <button class="chat-header-sidebar-toggle" onclick="toggleSidebar()" aria-label="Открыть меню">
                        <i class="fas fa-bars"></i>
                    </button>
                    <span class="chat-header-title" id="chatHeaderTitle">Новый чат</span>
                </div>
                <div class="chat-header-actions">
                    <button class="chat-header-btn" id="previewToggleBtn" onclick="togglePreview()" title="Предпросмотр" aria-label="Переключить предпросмотр">
                        <i class="fas fa-columns"></i>
                    </button>
                </div>
            </header>

            <div class="chat-messages" id="chatMessages">
                <div class="chat-welcome" id="chatWelcome">
                    <div class="chat-welcome-icon">U</div>
                    <h2>Чем могу помочь?</h2>
                    <p>Создавайте приложения, сайты, пишите код на любом языке — всё бесплатно и без ограничений</p>
                    <div class="chat-welcome-suggestions">
                        <div class="suggestion-card" onclick="useSuggestion('Создай лендинг для кофейни с тёмной темой и анимациями')">
                            <div class="suggestion-card-icon"><i class="fas fa-store"></i></div>
                            <div class="suggestion-card-text">Лендинг для кофейни с анимациями</div>
                        </div>
                        <div class="suggestion-card" onclick="useSuggestion('Создай приложение-калькулятор с красивым дизайном')">
                            <div class="suggestion-card-icon"><i class="fas fa-calculator"></i></div>
                            <div class="suggestion-card-text">Приложение-калькулятор</div>
                        </div>
                        <div class="suggestion-card" onclick="useSuggestion('Напиши на Python алгоритм сортировки пузырьком с комментариями')">
                            <div class="suggestion-card-icon"><i class="fab fa-python"></i></div>
                            <div class="suggestion-card-text">Код на Python — сортировка</div>
                        </div>
                        <div class="suggestion-card" onclick="useSuggestion('Создай дашборд аналитики с графиками и статистикой')">
                            <div class="suggestion-card-icon"><i class="fas fa-chart-bar"></i></div>
                            <div class="suggestion-card-text">Дашборд аналитики</div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="chat-input-area">
                <div class="chat-input-wrapper">
                    <div class="chat-files-preview hidden" id="filesPreview"></div>
                    <div class="chat-input-container">
                        <div class="chat-input-left">
                            <button class="chat-input-file-btn" onclick="document.getElementById('fileInput').click()" title="Прикрепить файл" aria-label="Прикрепить файл">
                                <i class="fas fa-paperclip"></i>
                            </button>
                        </div>
                        <textarea class="chat-input" id="chatInput" placeholder="Опиши, что хочешь создать..." rows="1" aria-label="Введите промпт"></textarea>
                        <button class="chat-send-btn" id="sendBtn" onclick="sendMessage()" disabled aria-label="Отправить сообщение">
                            <i class="fas fa-arrow-up"></i>
                        </button>
                    </div>
                    <div class="chat-input-hint">Umar AI бесплатен навсегда. Без лимитов. Без подписок.</div>
                </div>
                <input type="file" id="fileInput" multiple accept="image/*,.py,.js,.ts,.html,.css,.cpp,.c,.java,.txt,.json,.md,.csv" style="display:none" onchange="handleFiles(this.files)">
            </div>
        </div>

        <!-- Preview Panel -->
        <div class="preview-panel" id="previewPanel">
            <div class="preview-header">
                <span class="preview-title"><span class="preview-title-dot"></span> Preview</span>
                <div class="preview-url" id="previewUrl">
                    <i class="fas fa-lock" style="font-size:10px"></i>
                    <span class="preview-url-text" id="previewUrlText">local.umarai.app</span>
                </div>
                <button class="preview-close" onclick="togglePreview()" aria-label="Закрыть предпросмотр">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <iframe class="preview-frame" id="previewFrame" sandbox="allow-scripts allow-same-origin allow-forms allow-popups"></iframe>
        </div>
    </div>

    <!-- ========== Publish Modal ========== -->
    <div class="modal-overlay hidden" id="publishModal">
        <div class="modal" id="publishModalContent">
            <div class="modal-header">
                <span class="modal-title">Опубликовать проект</span>
                <button class="modal-close" onclick="closePublishModal()"><i class="fas fa-times"></i></button>
            </div>
            <div class="modal-body" id="publishModalBody">
                <div class="form-group">
                    <label class="form-label">Название проекта</label>
                    <input class="form-input" id="publishName" type="text" placeholder="my-awesome-app" maxlength="40">
                    <div class="form-hint">Будет использоваться в URL: имя.umarai.app</div>
                </div>
                <div class="form-group">
                    <label class="form-label">Домен</label>
                    <div class="form-input-prefix">
                        <span id="publishDomainPrefix">my-awesome-app.umarai.app</span>
                    </div>
                    <div class="form-hint">Домен формируется автоматически</div>
                </div>
            </div>
            <div class="modal-footer" id="publishModalFooter">
                <button class="modal-btn modal-btn-secondary" onclick="closePublishModal()">Отмена</button>
                <button class="modal-btn modal-btn-primary" onclick="confirmPublish()">Опубликовать</button>
            </div>
        </div>
    </div>

    <!-- ========== Profile Modal ========== -->
    <div class="modal-overlay hidden" id="profileModal">
        <div class="modal">
            <div class="modal-header">
                <span class="modal-title">Профиль</span>
                <button class="modal-close" onclick="closeProfile()"><i class="fas fa-times"></i></button>
            </div>
            <div class="modal-body">
                <div class="profile-content">
                    <div class="profile-avatar-large" id="profileAvatar">U</div>
                    <div class="profile-name" id="profileName">User</div>
                    <div class="profile-email" id="profileEmail">user@email.com</div>
                    <div class="profile-plan-badge">
                        <i class="fas fa-infinity"></i>
                        Бесплатный план — Без лимитов
                    </div>
                    <div class="profile-stats">
                        <div class="profile-stat">
                            <div class="profile-stat-value" id="statChats">0</div>
                            <div class="profile-stat-label">Чатов</div>
                        </div>
                        <div class="profile-stat">
                            <div class="profile-stat-value" id="statApps">0</div>
                            <div class="profile-stat-label">Приложений</div>
                        </div>
                        <div class="profile-stat">
                            <div class="profile-stat-value" id="statPublished">0</div>
                            <div class="profile-stat-label">Опубликовано</div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="modal-footer">
                <button class="modal-btn modal-btn-secondary" onclick="closeProfile();logout()">
                    <i class="fas fa-sign-out-alt" style="margin-right:6px"></i>Выйти
                </button>
                <button class="modal-btn modal-btn-primary" onclick="closeProfile()">Готово</button>
            </div>
        </div>
    </div>

    <!-- ========== Toast Container ========== -->
    <div class="toast-container" id="toastContainer"></div>

    <script>
    /* ==========================================================
       UMAR AI — Полноценный ИИ-ассистент для создания приложений
       ========================================================== */

    // ========== Состояние приложения ==========
    const APP_STATE = {
        user: null,
        chats: [],
        activeChatId: null,
        isGenerating: false,
        attachedFiles: [],
        lastGeneratedCode: null,
        lastGeneratedLanguage: null,
        previewOpen: false,
        sidebarOpen: true,
        publishedProjects: []
    };

    // ========== Данные пользователей для симуляции ==========
    const MOCK_GOOGLE_USERS = [
        { name: 'Александр Иванов', email: 'alex.ivanov@gmail.com', avatar: '#4285F4', initial: 'А' },
        { name: 'Мария Петрова', email: 'maria.petrova@gmail.com', avatar: '#EA4335', initial: 'М' },
        { name: 'Дмитрий Козлов', email: 'dmitry.kozlov@gmail.com', avatar: '#34A853', initial: 'Д' }
    ];
    const MOCK_APPLE_USERS = [
        { name: 'Елена Смирнова', email: 'elena.smirnova@icloud.com', avatar: '#a1a1a6', initial: 'Е' },
        { name: 'Артём Новиков', email: 'artem.novikov@icloud.com', avatar: '#555558', initial: 'А' }
    ];

    // ========== Инициализация ==========
    function init() {
        // Проверяем сохранённую сессию
        const savedUser = localStorage.getItem('umarai_user');
        const savedChats = localStorage.getItem('umarai_chats');
        const savedPublished = localStorage.getItem('umarai_published');

        if (savedUser) {
            APP_STATE.user = JSON.parse(savedUser);
            if (savedChats) APP_STATE.chats = JSON.parse(savedChats);
            if (savedPublished) APP_STATE.publishedProjects = JSON.parse(savedPublished);
            showMainApp();
        }

        // Настройка textarea авто-рост
        const input = document.getElementById('chatInput');
        input.addEventListener('input', () => {
            input.style.height = 'auto';
            input.style.height = Math.min(input.scrollHeight, 160) + 'px';
            document.getElementById('sendBtn').disabled = input.value.trim() === '' && APP_STATE.attachedFiles.length === 0;
        });

        // Enter для отправки
        input.addEventListener('keydown', (e) => {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                if (!document.getElementById('sendBtn').disabled) sendMessage();
            }
        });

        // Обновление домена при вводе имени проекта
        document.getElementById('publishName').addEventListener('input', (e) => {
            const val = e.target.value.toLowerCase().replace(/[^a-z0-9-]/g, '').replace(/-+/g, '-');
            document.getElementById('publishDomainPrefix').textContent = val + '.umarai.app';
        });

        // Drag & drop
        setupDragDrop();

        // Закрытие модалок по Escape
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') {
                closeAuthModals();
                closePublishModal();
                closeProfile();
            }
        });
    }

    // ========== Drag & Drop ==========
    function setupDragDrop() {
        let dragCounter = 0;
        const overlay = document.getElementById('dropOverlay');

        document.addEventListener('dragenter', (e) => {
            e.preventDefault();
            dragCounter++;
            if (APP_STATE.user) overlay.classList.remove('hidden');
        });
        document.addEventListener('dragleave', (e) => {
            e.preventDefault();
            dragCounter--;
            if (dragCounter === 0) overlay.classList.add('hidden');
        });
        document.addEventListener('dragover', (e) => e.preventDefault());
        document.addEventListener('drop', (e) => {
            e.preventDefault();
            dragCounter = 0;
            overlay.classList.add('hidden');
            if (APP_STATE.user && e.dataTransfer.files.length) {
                handleFiles(e.dataTransfer.files);
            }
        });
    }

    // ========== Авторизация ==========
    function showGoogleAuth() {
        const container = document.getElementById('googleAccounts');
        container.innerHTML = MOCK_GOOGLE_USERS.map((u, i) => `
            <div class="auth-account" onclick="loginWithUser(${JSON.stringify(u).replace(/"/g, '&quot;')}, 'google')">
                <div class="auth-account-avatar" style="background:${u.avatar}">${u.initial}</div>
                <div class="auth-account-info">
                    <div class="auth-account-name">${u.name}</div>
                    <div class="auth-account-email">${u.email}</div>
                </div>
            </div>
        `).join('');
        document.getElementById('googleAuthModal').classList.remove('hidden');
    }

    function showAppleAuth() {
        const container = document.getElementById('appleAccounts');
        container.innerHTML = MOCK_APPLE_USERS.map((u, i) => `
            <div class="auth-account" onclick="loginWithUser(${JSON.stringify(u).replace(/"/g, '&quot;')}, 'apple')">
                <div class="auth-account-avatar" style="background:${u.avatar}">${u.initial}</div>
                <div class="auth-account-info">
                    <div class="auth-account-name">${u.name}</div>
                    <div class="auth-account-email">${u.email}</div>
                </div>
            </div>
        `).join('');
        document.getElementById('appleAuthModal').classList.remove('hidden');
    }

    function closeAuthModals() {
        document.getElementById('googleAuthModal').classList.add('hidden');
        document.getElementById('appleAuthModal').classList.add('hidden');
    }

    function loginWithUser(user, provider) {
        closeAuthModals();
        user.provider = provider;
        user.loginTime = Date.now();
        APP_STATE.user = user;
        localStorage.setItem('umarai_user', JSON.stringify(user));
        showToast('success', `Добро пожаловать, ${user.name}!`);
        showMainApp();
    }

    function logout() {
        APP_STATE.user = null;
        APP_STATE.chats = [];
        APP_STATE.activeChatId = null;
        localStorage.removeItem('umarai_user');
        localStorage.removeItem('umarai_chats');
        document.getElementById('mainApp').classList.add('hidden');
        document.getElementById('loginScreen').classList.remove('hidden');
        closeProfile();
        showToast('info', 'Вы вышли из аккаунта');
    }

    function showMainApp() {
        document.getElementById('loginScreen').classList.add('hidden');
        document.getElementById('mainApp').classList.remove('hidden');
        updateProfileUI();
        renderChatHistory();
        if (APP_STATE.chats.length > 0) {
            loadChat(APP_STATE.chats[0].id);
        }
    }

    function updateProfileUI() {
        if (!APP_STATE.user) return;
        const u = APP_STATE.user;
        document.getElementById('sidebarAvatar').style.background = u.avatar;
        document.getElementById('sidebarAvatar').textContent = u.initial;
        document.getElementById('sidebarName').textContent = u.name;
        document.getElementById('profileAvatar').style.background = u.avatar;
        document.getElementById('profileAvatar').textContent = u.initial;
        document.getElementById('profileName').textContent = u.name;
        document.getElementById('profileEmail').textContent = u.email;
        document.getElementById('statChats').textContent = APP_STATE.chats.length;
        document.getElementById('statApps').textContent = APP_STATE.chats.reduce((a, c) => a + (c.hasApp ? 1 : 0), 0);
        document.getElementById('statPublished').textContent = APP_STATE.publishedProjects.length;
    }

    // ========== Профиль ==========
    function openProfile() {
        updateProfileUI();
        document.getElementById('profileModal').classList.remove('hidden');
    }
    function closeProfile() {
        document.getElementById('profileModal').classList.add('hidden');
    }

    // ========== Боковая панель ==========
    function toggleSidebar() {
        const sidebar = document.getElementById('sidebar');
        const overlay = document.getElementById('sidebarOverlay');
        APP_STATE.sidebarOpen = !APP_STATE.sidebarOpen;
        sidebar.classList.toggle('collapsed', !APP_STATE.sidebarOpen);
        if (window.innerWidth <= 768) {
            overlay.classList.toggle('active', APP_STATE.sidebarOpen);
        }
    }

    // ========== Чаты ==========
    function newChat() {
        const chat = {
            id: 'chat_' + Date.now(),
            title: 'Новый чат',
            messages: [],
            hasApp: false,
            createdAt: Date.now()
        };
        APP_STATE.chats.unshift(chat);
        APP_STATE.activeChatId = chat.id;
        saveChats();
        renderChatHistory();
        renderMessages();
        updateProfileUI();
        if (window.innerWidth <= 768) toggleSidebar();
    }

    function loadChat(chatId) {
        APP_STATE.activeChatId = chatId;
        renderChatHistory();
        renderMessages();
        if (window.innerWidth <= 768 && APP_STATE.sidebarOpen) toggleSidebar();
    }

    function deleteChat(chatId, e) {
        e.stopPropagation();
        APP_STATE.chats = APP_STATE.chats.filter(c => c.id !== chatId);
        if (APP_STATE.activeChatId === chatId) {
            APP_STATE.activeChatId = APP_STATE.chats.length > 0 ? APP_STATE.chats[0].id : null;
        }
        saveChats();
        renderChatHistory();
        renderMessages();
        updateProfileUI();
    }

    function getActiveChat() {
        return APP_STATE.chats.find(c => c.id === APP_STATE.activeChatId);
    }

    function saveChats() {
        localStorage.setItem('umarai_chats', JSON.stringify(APP_STATE.chats));
    }

    function renderChatHistory() {
        const container = document.getElementById('chatHistory');
        if (APP_STATE.chats.length === 0) {
            container.innerHTML = '<div style="padding:16px;text-align:center;font-size:13px;color:var(--text-muted)">Нет чатов</div>';
            return;
        }
        container.innerHTML = APP_STATE.chats.map(chat => `
            <div class="history-item ${chat.id === APP_STATE.activeChatId ? 'active' : ''}" onclick="loadChat('${chat.id}')">
                <i class="fas ${chat.hasApp ? 'fa-cube' : 'fa-message'} history-item-icon"></i>
                <span class="history-item-text">${escapeHtml(chat.title)}</span>
                <button class="history-item-delete" onclick="deleteChat('${chat.id}', event)" aria-label="Удалить чат">
                    <i class="fas fa-trash"></i>
                </button>
            </div>
        `).join('');
    }

    // ========== Рендер сообщений ==========
    function renderMessages() {
        const container = document.getElementById('chatMessages');
        const chat = getActiveChat();
        const welcome = document.getElementById('chatWelcome');

        if (!chat || chat.messages.length === 0) {
            welcome.classList.remove('hidden');
            // Удаляем все сообщения кроме welcome
            Array.from(container.children).forEach(child => {
                if (child !== welcome) child.remove();
            });
            document.getElementById('chatHeaderTitle').textContent = 'Новый чат';
            return;
        }

        welcome.classList.add('hidden');
        document.getElementById('chatHeaderTitle').textContent = chat.title;

        // Очищаем и рендерим сообщения
        const fragment = document.createDocumentFragment();
        chat.messages.forEach(msg => {
            fragment.appendChild(createMessageElement(msg));
        });
        container.innerHTML = '';
        container.appendChild(fragment);
        scrollToBottom();
    }

    function createMessageElement(msg) {
        const div = document.createElement('div');

        if (msg.role === 'user') {
            div.className = 'message message-user';
            let content = `<div class="message-user-bubble">${escapeHtml(msg.text)}`;
            if (msg.files && msg.files.length > 0) {
                content += msg.files.map(f => {
                    if (f.type === 'image') return `<br><img src="${f.data}" class="chat-image-preview" alt="${escapeHtml(f.name)}">`;
                    return `<br><div class="chat-file-preview"><i class="fas fa-file"></i><span class="chat-file-preview-name">${escapeHtml(f.name)}</span></div>`;
                }).join('');
            }
            content += '</div>';
            div.innerHTML = content;
        } else {
            div.className = 'message message-ai';
            let html = '<div class="message-ai-avatar">U</div><div class="message-ai-content">';

            if (msg.plan) {
                html += `<div class="message-plan">
                    <div class="message-plan-title"><i class="fas fa-clipboard-list"></i> PLAN</div>
                    <ul class="message-plan-items">
                        ${msg.plan.map(item => `<li><i class="fas fa-check-circle"></i>${escapeHtml(item)}</li>`).join('')}
                    </ul>
                </div>`;
            }

            if (msg.text) {
                html += `<div class="message-ai-text">${msg.text}</div>`;
            }

            if (msg.code) {
                html += `<div class="message-build-title"><i class="fas fa-code"></i> BUILD</div>`;
                html += createCodeBlockHtml(msg.code, msg.language || 'html');
            }

            if (msg.code) {
                html += `<div class="message-actions">
                    <button class="msg-action-btn primary" onclick="previewCode(this)" data-code="${btoa(unescape(encodeURIComponent(msg.code)))}"><i class="fas fa-eye"></i> Preview</button>
                    <button class="msg-action-btn" onclick="downloadHTML(this)" data-code="${btoa(unescape(encodeURIComponent(msg.code)))}"><i class="fas fa-download"></i> Скачать HTML</button>
                    <button class="msg-action-btn" onclick="openPublishModal(this)" data-code="${btoa(unescape(encodeURIComponent(msg.code)))}"><i class="fas fa-rocket"></i> Опубликовать</button>
                    <button class="msg-action-btn" onclick="copyCode(this)" data-code="${btoa(unescape(encodeURIComponent(msg.code)))}"><i class="fas fa-copy"></i> Копировать код</button>
                </div>`;
            }

            html += '</div>';
            div.innerHTML = html;
        }

        return div;
    }

    function createCodeBlockHtml(code, lang) {
        const highlighted = highlightSyntax(code, lang);
        return `<div class="code-block-wrapper">
            <div class="code-block-header">
                <span class="code-block-lang">${lang}</span>
                <button class="code-block-copy" onclick="copyCodeBlock(this)"><i class="fas fa-copy"></i> Копировать</button>
            </div>
            <pre class="code-block">${highlighted}</pre>
        </div>`;
    }

    // ========== Подсветка синтаксиса (базовая) ==========
    function highlightSyntax(code, lang) {
        let escaped = escapeHtml(code);
        // Комментарии
        escaped = escaped.replace(/(\/\/.*$)/gm, '<span class="cm">$1</span>');
        escaped = escaped.replace(/(\/\*[\s\S]*?\*\/)/g, '<span class="cm">$1</span>');
        escaped = escaped.replace(/(&lt;!--[\s\S]*?--&gt;)/g, '<span class="cm">$1</span>');
        // Строки
        escaped = escaped.replace(/(&quot;[^&]*?&quot;)/g, '<span class="str">$1</span>');
        escaped = escaped.replace(/(&#039;[^&]*?&#039;)/g, '<span class="str">$1</span>');
        escaped = escaped.replace(/('(?:[^'\\]|\\.)*')/g, '<span class="str">$1</span>');
        escaped = escaped.replace(/("(?:[^"\\]|\\.)*")/g, '<span class="str">$1</span>');
        // Ключевые слова
        const keywords = ['function','const','let','var','if','else','for','while','return','class','import','export','from','default','async','await','try','catch','throw','new','this','switch','case','break','continue','typeof','instanceof','in','of','def','print','self','True','False','None','int','float','str','void','public','private','protected','static','include','using','namespace','template','struct','enum','extends','implements','interface','abstract','final','super','yield','lambda','with','as','assert','pass','raise','except','finally','global','nonlocal'];
        keywords.forEach(kw => {
            const re = new RegExp('\\b(' + kw + ')\\b', 'g');
            escaped = escaped.replace(re, '<span class="kw">$1</span>');
        });
        // Числа
        escaped = escaped.replace(/\b(\d+\.?\d*)\b/g, '<span class="num">$1</span>');
        // HTML теги (для HTML)
        if (lang === 'html') {
            escaped = escaped.replace(/(&lt;\/?)([\w-]+)/g, '$1<span class="tag">$2</span>');
            escaped = escaped.replace(/\s([\w-]+)=/g, ' <span class="attr">$1</span>=');
        }
        return escaped;
    }

    // ========== Отправка сообщений ==========
    async function sendMessage() {
        const input = document.getElementById('chatInput');
        const text = input.value.trim();
        if (!text && APP_STATE.attachedFiles.length === 0) return;
        if (APP_STATE.isGenerating) return;

        // Создаём чат если нужно
        if (!APP_STATE.activeChatId) {
            newChat();
        }

        const chat = getActiveChat();
        if (!chat) return;

        // Формируем сообщение пользователя
        const userMsg = { role: 'user', text: text };
        if (APP_STATE.attachedFiles.length > 0) {
            userMsg.files = APP_STATE.attachedFiles.map(f => ({ name: f.name, type: f.type, data: f.data }));
        }
        chat.messages.push(userMsg);

        // Обновляем заголовок чата
        if (chat.messages.length === 1) {
            chat.title = text.length > 50 ? text.substring(0, 50) + '...' : text;
            renderChatHistory();
            document.getElementById('chatHeaderTitle').textContent = chat.title;
        }

        // Очищаем ввод
        input.value = '';
        input.style.height = 'auto';
        document.getElementById('sendBtn').disabled = true;
        clearAttachedFiles();

        // Рендерим сообщение пользователя
        const welcome = document.getElementById('chatWelcome');
        welcome.classList.add('hidden');
        const container = document.getElementById('chatMessages');
        container.appendChild(createMessageElement(userMsg));
        scrollToBottom();

        // Показываем thinking
        APP_STATE.isGenerating = true;
        const thinkingEl = showThinking(container);

        // Генерируем ответ
        try {
            const response = await generateResponse(text, userMsg.files);
            thinkingEl.remove();

            // Добавляем ответ в чат
            chat.messages.push(response);
            if (response.code && response.language === 'html') {
                chat.hasApp = true;
            }
            saveChats();
            renderChatHistory();
            updateProfileUI();

            // Рендерим ответ с анимацией
            await renderAIResponse(response, container);
        } catch (err) {
            thinkingEl.remove();
            const errorMsg = { role: 'ai', text: `<p>Произошла ошибка при генерации. Попробуйте ещё раз.</p>` };
            chat.messages.push(errorMsg);
            saveChats();
            container.appendChild(createMessageElement(errorMsg));
            scrollToBottom();
        }

        APP_STATE.isGenerating = false;
    }

    function showThinking(container) {
        const div = document.createElement('div');
        div.className = 'thinking-indicator';
        div.innerHTML = `
            <div class="message-ai-avatar">U</div>
            <div class="thinking-dots">
                <div class="thinking-dot"></div>
                <div class="thinking-dot"></div>
                <div class="thinking-dot"></div>
            </div>
            <span class="thinking-label">Думаю...</span>
        `;
        container.appendChild(div);
        scrollToBottom();
        return div;
    }

    async function renderAIResponse(msg, container) {
        const div = document.createElement('div');
        div.className = 'message message-ai';
        let html = '<div class="message-ai-avatar">U</div><div class="message-ai-content">';

        // Фаза PLAN
        if (msg.plan) {
            html += `<div class="message-plan">
                <div class="message-plan-title"><i class="fas fa-clipboard-list"></i> PLAN</div>
                <ul class="message-plan-items">
                    ${msg.plan.map(item => `<li><i class="fas fa-check-circle"></i>${escapeHtml(item)}</li>`).join('')}
                </ul>
            </div>`;
        }

        // Прогресс-бар
        html += `<div class="gen-progress"><div class="gen-progress-bar" id="genProgress_${Date.now()}"></div></div>`;

        // Текст ответа
        if (msg.text) {
            html += `<div class="message-ai-text streaming-cursor" id="streamingText">${msg.text}</div>`;
        }

        // Фаза BUILD с кодом
        if (msg.code) {
            html += `<div class="message-build-title" style="display:none" id="buildTitle"><i class="fas fa-code"></i> BUILD</div>`;
            html += `<div style="display:none" id="codeContainer">${createCodeBlockHtml(msg.code, msg.language || 'html')}</div>`;
            html += `<div class="message-actions" style="display:none" id="actionButtons">
                <button class="msg-action-btn primary" onclick="previewCode(this)" data-code="${btoa(unescape(encodeURIComponent(msg.code)))}"><i class="fas fa-eye"></i> Preview</button>
                <button class="msg-action-btn" onclick="downloadHTML(this)" data-code="${btoa(unescape(encodeURIComponent(msg.code)))}"><i class="fas fa-download"></i> Скачать HTML</button>
                <button class="msg-action-btn" onclick="openPublishModal(this)" data-code="${btoa(unescape(encodeURIComponent(msg.code)))}"><i class="fas fa-rocket"></i> Опубликовать</button>
                <button class="msg-action-btn" onclick="copyCode(this)" data-code="${btoa(unescape(encodeURIComponent(msg.code)))}"><i class="fas fa-copy"></i> Копировать код</button>
            </div>`;
        }

        html += '</div>';
        div.innerHTML = html;
        container.appendChild(div);
        scrollToBottom();

        // Анимация прогресс-бара
        const progressBar = div.querySelector('[id^="genProgress"]');
        if (progressBar) {
            await animateProgress(progressBar);
        }

        // Показываем BUILD секцию
        const buildTitle = div.querySelector('#buildTitle');
        const codeContainer = div.querySelector('#codeContainer');
        const actionButtons = div.querySelector('#actionButtons');

        if (msg.code && buildTitle) {
            await delay(300);
            buildTitle.style.display = 'flex';
            buildTitle.style.animation = 'msgAppear 0.3s ease';
            scrollToBottom();
            await delay(200);
            codeContainer.style.display = 'block';
            codeContainer.style.animation = 'msgAppear 0.3s ease';
            scrollToBottom();
            await delay(200);
            actionButtons.style.display = 'flex';
            actionButtons.style.animation = 'msgAppear 0.3s ease';
            scrollToBottom();
        }

        // Убираем курсор стриминга
        const streamingText = div.querySelector('#streamingText');
        if (streamingText) {
            await delay(500);
            streamingText.classList.remove('streaming-cursor');
        }

        // Убираем прогресс-бар
        if (progressBar) {
            await delay(300);
            progressBar.parentElement.remove();
        }
    }

    async function animateProgress(bar) {
        const steps = [15, 30, 50, 70, 85, 95, 100];
        for (const val of steps) {
            bar.style.width = val + '%';
            await delay(150 + Math.random() * 200);
        }
    }

    function delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }

    // ========== Генерация ответа ИИ ==========
    async function generateResponse(prompt, files) {
        // Добавляем задержку для реалистичности
        const modelDelay = getModelDelay();
        await delay(modelDelay);

        const lower = prompt.toLowerCase();
        let language = detectLanguage(lower);
        let appType = detectAppType(lower);

        // Если прикреплены файлы с кодом, учитываем их
        if (files && files.length > 0) {
            files.forEach(f => {
                if (f.name.endsWith('.py')) language = 'python';
                else if (f.name.endsWith('.cpp') || f.name.endsWith('.c')) language = 'cpp';
                else if (f.name.endsWith('.java')) language = 'java';
                else if (f.name.endsWith('.js') || f.name.endsWith('.ts')) language = 'javascript';
            });
        }

        // Общие вопросы (не код)
        if (isGeneralQuestion(lower)) {
            return {
                role: 'ai',
                text: generateGeneralAnswer(prompt),
                plan: null,
                code: null,
                language: null
            };
        }

        // Генерация кода на языках программирования
        if (language !== 'html') {
            const code = generateCodeForLanguage(language, prompt, appType);
            const plan = [
                `Анализ запроса и выбор подходящего решения`,
                `Написание кода на ${language.toUpperCase()}`,
                `Добавление комментариев и оптимизация`,
                `Проверка корректности кода`
            ];
            return {
                role: 'ai',
                text: `<p>Вот код на <strong>${language.toUpperCase()}</strong>, который решает вашу задачу:</p>`,
                plan: plan,
                code: code,
                language: language
            };
        }

        // Генерация HTML приложения/сайта
        const plan = generatePlan(appType, prompt);
        const code = generateHTMLApp(appType, prompt);
        const projectName = extractProjectName(prompt, appType);

        return {
            role: 'ai',
            text: `<p>Я создал <strong>${projectName}</strong> для вас. Вот что включено:</p><ul>${plan.map(p => `<li>${p}</li>`).join('')}</ul>`,
            plan: plan,
            code: code,
            language: 'html'
        };
    }

    function getModelDelay() {
        const model = document.getElementById('modelSelect').value;
        const delays = {
            'gpt-5.4': 1200, 'gpt-5.3': 1400, 'gpt-5.2': 1600, 'gpt-5.1': 1800,
            'claude-4-opus': 1300, 'claude-4-sonnet': 1500, 'claude-4-haiku': 1000,
            'claude-3.5-sonnet': 1600, 'claude-3.5-haiku': 1100, 'claude-3-opus': 1800, 'claude-3-sonnet': 1700,
            'gemini-3-pro': 1200, 'gemini-3.1-pro': 1400,
            'grok-4': 1100, 'qwem-3-max': 1300, 'kimi-k2': 1500,
            'deepseek-v3': 1400, 'llama-3.3': 1600
        };
        return (delays[model] || 1500) + Math.random() * 500;
    }

    function detectLanguage(text) {
        if (text.includes('python') || text.includes('питон') || text.includes('скрипт python')) return 'python';
        if (text.includes('c++') || text.includes('cpp') || text.includes('си++')) return 'cpp';
        if (text.includes('c#') || text.includes('csharp')) return 'cpp';
        if (text.includes('java ') && !text.includes('javascript')) return 'java';
        if (text.includes('javascript') || text.includes(' js ') || text.includes('node')) return 'javascript';
        return 'html';
    }

    function detectAppType(text) {
        if (text.includes('лендинг') || text.includes('landing') || text.includes('сайт') || text.includes('website') || text.includes('главную страницу')) return 'landing';
        if (text.includes('дашборд') || text.includes('dashboard') || text.includes('панель') || text.includes('аналитик')) return 'dashboard';
        if (text.includes('todo') || text.includes('задач') || text.includes('дела') || text.includes('список дел')) return 'todo';
        if (text.includes('игр') || text.includes('game') || text.includes('тетрис') || text.includes('змейк')) return 'game';
        if (text.includes('калькулятор') || text.includes('calculator')) return 'calculator';
        if (text.includes('портфолио') || text.includes('portfolio') || text.includes('резюме')) return 'portfolio';
        if (text.includes('погод') || text.includes('weather')) return 'weather';
        if (text.includes('чат') || text.includes('chat') || text.includes('мессенджер')) return 'chat';
        if (text.includes('магазин') || text.includes('shop') || text.includes('ecommerce') || text.includes('торг') || text.includes('товар')) return 'ecommerce';
        if (text.includes('блог') || text.includes('blog') || text.includes('статьи')) return 'blog';
        if (text.includes('форм') || text.includes('form') || text.includes('регистрац') || text.includes('логин')) return 'form';
        return 'generic';
    }

    function isGeneralQuestion(text) {
        const qWords = ['что такое', 'кто такой', 'как работает', 'объясни', 'расскажи', 'что значит', 'why', 'what is', 'how does', 'explain', 'каково', 'чем отличается'];
        return qWords.some(w => text.includes(w)) && !text.includes('создай') && !text.includes('напиши') && !text.includes('сделай') && !text.includes('построй') && !text.includes('generate') && !text.includes('build');
    }

    function extractProjectName(prompt, appType) {
        const names = {
            landing: 'Лендинг', dashboard: 'Дашборд', todo: 'Todo App',
            game: 'Игра', calculator: 'Калькулятор', portfolio: 'Портфолио',
            weather: 'Погода', chat: 'Чат', ecommerce: 'Магазин',
            blog: 'Блог', form: 'Форма', generic: 'Приложение'
        };
        return names[appType] || 'Приложение';
    }

    function generatePlan(appType, prompt) {
        const plans = {
            landing: [
                'Современный hero-блок с анимированным фоном и заголовком',
                'Секция преимуществ с иконками и описаниями',
                'Галерея/портфолио с hover-эффектами',
                'Форма обратной связи с валидацией',
                'Footer с ссылками и контактами',
                'Адаптивный дизайн для мобильных устройств'
            ],
            dashboard: [
                'Боковая навигация с иконками и активным состоянием',
                'Карточки с ключевыми метриками (KPI)',
                'Интерактивные графики с анимациями',
                'Таблица данных с сортировкой и фильтрами',
                'Уведомления и профиль пользователя',
                'Тёмная тема с плавными переходами'
            ],
            todo: [
                'Поле ввода для новых задач с кнопкой добавления',
                'Список задач с чекбоксами и анимацией выполнения',
                'Фильтры: Все / Активные / Выполненные',
                'Счётчик оставшихся задач',
                'Кнопка очистки выполненных задач',
                'Сохранение данных в localStorage'
            ],
            game: [
                'Игровое поле/холст с анимацией',
                'Система счёта и уровней',
                'Управление с клавиатуры и мыши',
                'Звуковые эффекты и визуальная обратная связь',
                'Экран старта и Game Over',
                'Адаптивное управление для мобильных'
            ],
            calculator: [
                'Дисплей с историей вычислений',
                'Кнопки цифр с hover-анимациями',
                'Базовые операции: +, -, ×, ÷',
                'Дополнительные функции: %, ±, C',
                'Поддержка цепочки вычислений',
                'Клавиатурный ввод'
            ],
            portfolio: [
                'Hero-секция с именем и должностью',
                'Навигация с плавным скроллом',
                'Секция навыков с прогресс-барами',
                'Галерея проектов с описаниями',
                'Контактная форма',
                'Анимации при скролле'
            ],
            weather: [
                'Поиск города с автодополнением',
                'Текущая погода с иконкой и температурой',
                'Прогноз на 5 дней',
                'Влажность, ветер, давление',
                'Анимированный фон в зависимости от погоды',
                'Сохранение последнего города'
            ],
            chat: [
                'Список контактов/чатов слева',
                'Область сообщений с пузырьками',
                'Поле ввода с кнопкой отправки',
                'Индикатор набора текста',
                'Метка времени у сообщений',
                'Адаптивный дизайн'
            ],
            ecommerce: [
                'Шапка с логотипом, поиском и корзиной',
                'Карусель товаров на главной',
                'Карточки товаров с ценой и кнопкой',
                'Корзина с подсчётом итога',
                'Фильтры по категориям и цене',
                'Страница товара с галереей'
            ],
            blog: [
                'Шапка с навигацией и поиском',
                'Сетка статей с превью-изображениями',
                'Теги и категории',
                'Пагинация',
                'Страница статьи с форматированием',
                'Боковая панель с популярными постами'
            ],
            form: [
                'Поля ввода с валидацией в реальном времени',
                'Выпадающие списки и чекбоксы',
                'Индикаторы силы пароля',
                'Кастомные переключатели',
                'Сообщение об успешной отправке',
                'Анимации переходов между шагами'
            ],
            generic: [
                'Анализ требований из промпта',
                'Разработка структуры и компонент',
                'Создание интерактивного интерфейса',
                'Добавление анимаций и переходов',
                'Адаптивный дизайн',
                'Оптимизация производительности'
            ]
        };
        return plans[appType] || plans.generic;
    }

    // ========== Генерация HTML приложений ==========
    function generateHTMLApp(appType, prompt) {
        const theme = getThemeFromPrompt(prompt);
        const appName = extractProjectName(prompt, appType);

        switch (appType) {
            case 'landing': return genLanding(prompt, theme);
            case 'dashboard': return genDashboard(prompt, theme);
            case 'todo': return genTodo(prompt, theme);
            case 'game': return genGame(prompt, theme);
            case 'calculator': return genCalculator(prompt, theme);
            case 'portfolio': return genPortfolio(prompt, theme);
            case 'weather': return genWeather(prompt, theme);
            case 'chat': return genChatApp(prompt, theme);
            case 'ecommerce': return genEcommerce(prompt, theme);
            case 'blog': return genBlog(prompt, theme);
            case 'form': return genForm(prompt, theme);
            default: return genGenericApp(prompt, theme, appName);
        }
    }

    function getThemeFromPrompt(prompt) {
        const lower = prompt.toLowerCase();
        if (lower.includes('тёмн') || lower.includes('dark') || lower.includes('ночь') || lower.includes('чёрн')) return 'dark';
        if (lower.includes('светл') || lower.includes('light') || lower.includes('бел') || lower.includes('minimal')) return 'light';
        if (lower.includes('неон') || lower.includes('neon') || lower.includes('кибер')) return 'neon';
        if (lower.includes('золот') || lower.includes('gold') || lower.includes('премиум') || lower.includes('luxury')) return 'gold';
        if (lower.includes('зелён') || lower.includes('green') || lower.includes('эко') || lower.includes('nature')) return 'green';
        if (lower.includes('красн') || lower.includes('red') || lower.includes('огн')) return 'red';
        return 'dark';
    }

    function getThemeColors(theme) {
        const themes = {
            dark: { bg: '#0f0f14', card: '#1a1a24', text: '#f0f0f5', muted: '#8888aa', accent: '#fbbf24', border: '#2a2a3a', gradient1: '#fbbf24', gradient2: '#f97316' },
            light: { bg: '#fafafa', card: '#ffffff', text: '#1a1a2e', muted: '#6b7280', accent: '#0ea5e9', border: '#e5e7eb', gradient1: '#0ea5e9', gradient2: '#6366f1' },
            neon: { bg: '#0a0a12', card: '#12121e', text: '#e0e0f0', muted: '#7777aa', accent: '#00ff88', border: '#1e1e35', gradient1: '#00ff88', gradient2: '#00bbff' },
            gold: { bg: '#0c0a08', card: '#1a1710', text: '#f5f0e8', muted: '#aa9966', accent: '#d4a853', border: '#2a2518', gradient1: '#d4a853', gradient2: '#b8860b' },
            green: { bg: '#0a120a', card: '#142014', text: '#e8f0e8', muted: '#66aa66', accent: '#22c55e', border: '#1e3a1e', gradient1: '#22c55e', gradient2: '#16a34a' },
            red: { bg: '#120a0a', card: '#201414', text: '#f0e8e8', muted: '#aa6666', accent: '#ef4444', border: '#3a1e1e', gradient1: '#ef4444', gradient2: '#dc2626' }
        };
        return themes[theme] || themes.dark;
    }

    function wrapHTML(body, theme, title = 'Umar AI App') {
        const t = getThemeColors(theme);
        return `<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>${title}</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Space Grotesk',sans-serif;background:${t.bg};color:${t.text};min-height:100vh;-webkit-font-smoothing:antialiased}
::-webkit-scrollbar{width:6px}::-webkit-scrollbar-track{background:transparent}::-webkit-scrollbar-thumb{background:${t.border};border-radius:3px}
 ${body.includes('@keyframes') ? '' : ''}
</style>
</head>
<body>
 ${body}
</body>
</html>`;
    }

    // --- Лендинг ---
    function genLanding(prompt, theme) {
        const t = getThemeColors(theme);
        const subject = extractSubject(prompt, 'кофейню');
        return wrapHTML(`
<style>
.hero{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:40px 20px;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;width:600px;height:600px;background:radial-gradient(circle,${t.accent}22,transparent 70%);border-radius:50%;top:-100px;right:-200px;animation:float 8s ease-in-out infinite alternate}
.hero::after{content:'';position:absolute;width:400px;height:400px;background:radial-gradient(circle,${t.gradient2}18,transparent 70%);border-radius:50%;bottom:-100px;left:-100px;animation:float 10s ease-in-out infinite alternate-reverse}
@keyframes float{0%{transform:translate(0,0) scale(1)}100%{transform:translate(30px,-20px) scale(1.1)}}
.hero-badge{display:inline-flex;align-items:center;gap:6px;padding:6px 16px;border-radius:20px;border:1px solid ${t.accent}33;background:${t.accent}11;font-size:13px;color:${t.accent};margin-bottom:24px;animation:fadeInUp 0.6s ease}
.hero h1{font-size:clamp(36px,6vw,64px);font-weight:700;line-height:1.1;margin-bottom:20px;letter-spacing:-1px;animation:fadeInUp 0.6s ease 0.1s both;background:linear-gradient(135deg,${t.text},${t.accent});-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.hero p{font-size:18px;color:${t.muted};max-width:560px;line-height:1.6;margin-bottom:36px;animation:fadeInUp 0.6s ease 0.2s both}
.hero-buttons{display:flex;gap:12px;flex-wrap:wrap;justify-content:center;animation:fadeInUp 0.6s ease 0.3s both}
.btn{padding:14px 28px;border-radius:12px;font-size:15px;font-weight:600;cursor:pointer;transition:all 0.3s ease;text-decoration:none;display:inline-flex;align-items:center;gap:8px}
.btn-primary{background:${t.accent};color:#000;border:none}
.btn-primary:hover{transform:translateY(-2px);box-shadow:0 8px 24px ${t.accent}44}
.btn-outline{background:transparent;color:${t.text};border:1px solid ${t.border}}
.btn-outline:hover{border-color:${t.accent};background:${t.accent}11}
.features{padding:80px 20px;max-width:1100px;margin:0 auto}
.features h2{text-align:center;font-size:32px;font-weight:700;margin-bottom:12px;letter-spacing:-0.5px}
.features-sub{text-align:center;color:${t.muted};font-size:15px;margin-bottom:48px}
.features-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:20px}
.feature-card{padding:28px;border-radius:16px;background:${t.card};border:1px solid ${t.border};transition:all 0.3s ease}
.feature-card:hover{transform:translateY(-4px);border-color:${t.accent};box-shadow:0 8px 32px rgba(0,0,0,0.3)}
.feature-icon{width:48px;height:48px;border-radius:12px;background:${t.accent}15;display:flex;align-items:center;justify-content:center;font-size:20px;color:${t.accent};margin-bottom:16px}
.feature-card h3{font-size:17px;font-weight:600;margin-bottom:8px}
.feature-card p{font-size:14px;color:${t.muted};line-height:1.6}
.gallery{padding:80px 20px;max-width:1100px;margin:0 auto}
.gallery h2{text-align:center;font-size:32px;font-weight:700;margin-bottom:48px;letter-spacing:-0.5px}
.gallery-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:16px}
.gallery-item{border-radius:16px;overflow:hidden;aspect-ratio:4/3;position:relative;cursor:pointer}
.gallery-item img{width:100%;height:100%;object-fit:cover;transition:transform 0.5s ease}
.gallery-item:hover img{transform:scale(1.1)}
.gallery-item::after{content:'';position:absolute;inset:0;background:linear-gradient(to top,rgba(0,0,0,0.5),transparent);opacity:0;transition:opacity 0.3s}
.gallery-item:hover::after{opacity:1}
.cta{padding:80px 20px;text-align:center}
.cta-box{max-width:600px;margin:0 auto;padding:48px;border-radius:20px;background:linear-gradient(135deg,${t.accent}15,${t.gradient2}10);border:1px solid ${t.accent}22}
.cta-box h2{font-size:28px;font-weight:700;margin-bottom:12px}
.cta-box p{color:${t.muted};margin-bottom:28px;font-size:15px}
footer{padding:32px 20px;text-align:center;border-top:1px solid ${t.border};color:${t.muted};font-size:13px}
@keyframes fadeInUp{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}
</style>
<section class="hero">
<div class="hero-badge"><i class="fas fa-sparkles"></i> Добро пожаловать</div>
<h1>${subject.charAt(0).toUpperCase() + subject.slice(1)}</h1>
<p>Откройте для себя уникальную атмосферу и неповторимый вкус. Создано с любовью к деталям.</p>
<div class="hero-buttons">
<a class="btn btn-primary" href="#">Начать <i class="fas fa-arrow-right"></i></a>
<a class="btn btn-outline" href="#">Узнать больше</a>
</div>
</section>
<section class="features">
<h2>Почему выбирают нас</h2>
<p class="features-sub">Каждая деталь продумана для вашего комфорта</p>
<div class="features-grid">
<div class="feature-card"><div class="feature-icon"><i class="fas fa-star"></i></div><h3>Премиум качество</h3><p>Только лучшие ингредиенты и проверенные рецептуры для каждого заказа</p></div>
<div class="feature-card"><div class="feature-icon"><i class="fas fa-bolt"></i></div><h3>Быстрый сервис</h3><p>Ваш заказ будет готов за считанные минуты, без лишнего ожидания</p></div>
<div class="feature-card"><div class="feature-icon"><i class="fas fa-heart"></i></div><h3>С заботой о вас</h3><p>Индивидуальный подход к каждому гостю и внимание к деталям</p></div>
</div>
</section>
<section class="gallery">
<h2>Наша галерея</h2>
<div class="gallery-grid">
<div class="gallery-item"><img src="https://picsum.photos/seed/uma1/480/360.jpg" alt="Gallery 1"></div>
<div class="gallery-item"><img src="https://picsum.photos/seed/uma2/480/360.jpg" alt="Gallery 2"></div>
<div class="gallery-item"><img src="https://picsum.photos/seed/uma3/480/360.jpg" alt="Gallery 3"></div>
<div class="gallery-item"><img src="https://picsum.photos/seed/uma4/480/360.jpg" alt="Gallery 4"></div>
</div>
</section>
<section class="cta"><div class="cta-box"><h2>Готовы начать?</h2><p>Присоединяйтесь к нам прямо сейчас и получите скидку 20% на первый заказ</p><a class="btn btn-primary" href="#">Получить скидку</a></div></section>
<footer>Создано с помощью Umar AI</footer>
`, theme, subject.charAt(0).toUpperCase() + subject.slice(1));
    }

    // --- Дашборд ---
    function genDashboard(prompt, theme) {
        const t = getThemeColors(theme);
        return wrapHTML(`
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{display:flex;min-height:100vh}
.sidebar{width:240px;background:${t.card};border-right:1px solid ${t.border};padding:20px 0;display:flex;flex-direction:column}
.sidebar-logo{padding:0 20px 20px;font-size:18px;font-weight:700;display:flex;align-items:center;gap:8px}
.sidebar-logo span{color:${t.accent}}
.nav-item{display:flex;align-items:center;gap:10px;padding:10px 20px;color:${t.muted};cursor:pointer;transition:all 0.2s;font-size:14px}
.nav-item:hover,.nav-item.active{color:${t.text};background:${t.accent}11}
.nav-item.active{border-right:3px solid ${t.accent};color:${t.accent}}
.nav-item i{width:20px;text-align:center}
.main{flex:1;padding:24px;overflow-y:auto}
.topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:28px}
.topbar h1{font-size:24px;font-weight:700}
.top
