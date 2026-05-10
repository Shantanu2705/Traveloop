.loopie-bot-container {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 9999;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
}

.loopie-bot-launcher {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background: linear-gradient(135deg, #0ea5e9, #2563eb);
  color: white;
  border: none;
  box-shadow: 0 4px 14px rgba(37, 99, 235, 0.4);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.loopie-bot-launcher:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 20px rgba(37, 99, 235, 0.6);
}

.launcher-icon {
  font-size: 28px;
}

.loopie-bot-window {
  width: 350px;
  height: 500px;
  background: #ffffff;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  border: 1px solid #e5e7eb;
}

.loopie-bot-header {
  background: linear-gradient(135deg, #0ea5e9, #2563eb);
  color: white;
  padding: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-info {
  display: flex;
  align-items: center;
  gap: 12px;
}

.bot-avatar {
  font-size: 24px;
  background: rgba(255, 255, 255, 0.2);
  padding: 8px;
  border-radius: 50%;
}

.header-info h4 {
  margin: 0;
  font-size: 16px;
  font-weight: 600;
}

.header-info p {
  margin: 0;
  font-size: 12px;
  opacity: 0.8;
}

.close-bot {
  background: none;
  border: none;
  color: white;
  font-size: 24px;
  cursor: pointer;
  opacity: 0.8;
  transition: opacity 0.2s;
}

.close-bot:hover {
  opacity: 1;
}

.loopie-bot-messages {
  flex: 1;
  padding: 16px;
  overflow-y: auto;
  background-color: #f9fafb;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.message-row {
  display: flex;
  width: 100%;
}

.message-row.bot {
  justify-content: flex-start;
}

.message-row.user {
  justify-content: flex-end;
}

.message-bubble {
  max-width: 80%;
  padding: 12px 16px;
  border-radius: 16px;
  font-size: 14px;
  line-height: 1.5;
  color: #1f2937;
}

.message-bubble.bot {
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-bottom-left-radius: 4px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}

.message-bubble.user {
  background: #2563eb;
  color: white;
  border-bottom-right-radius: 4px;
  box-shadow: 0 2px 4px rgba(37, 99, 235, 0.2);
}

.message-bubble p {
  margin: 0;
}

.message-options {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-top: 12px;
}

.message-options button {
  background: #eff6ff;
  border: 1px solid #bfdbfe;
  color: #1d4ed8;
  padding: 8px 12px;
  border-radius: 8px;
  font-size: 13px;
  cursor: pointer;
  transition: all 0.2s;
  text-align: left;
}

.message-options button:hover {
  background: #dbeafe;
  border-color: #93c5fd;
}

.message-images {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 12px;
}

.image-card {
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  position: relative;
}

.image-card img {
  width: 100%;
  height: 140px;
  object-fit: cover;
  display: block;
}

.image-card span {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0,0,0,0.8));
  color: white;
  padding: 8px 12px;
  font-size: 12px;
  font-weight: 500;
}

.loopie-bot-input {
  display: flex;
  padding: 12px;
  background: #ffffff;
  border-top: 1px solid #e5e7eb;
  gap: 8px;
}

.loopie-bot-input input {
  flex: 1;
  padding: 10px 14px;
  border: 1px solid #d1d5db;
  border-radius: 20px;
  outline: none;
  font-size: 14px;
  transition: border-color 0.2s;
}

.loopie-bot-input input:focus {
  border-color: #2563eb;
}

.loopie-bot-input button {
  background: #2563eb;
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.2s;
}

.loopie-bot-input button:hover {
  background: #1d4ed8;
}

/* Scrollbar styles */
.loopie-bot-messages::-webkit-scrollbar {
  width: 6px;
}
.loopie-bot-messages::-webkit-scrollbar-track {
  background: transparent;
}
.loopie-bot-messages::-webkit-scrollbar-thumb {
  background: #d1d5db;
  border-radius: 3px;
}
.loopie-bot-messages::-webkit-scrollbar-thumb:hover {
  background: #9ca3af;
}

@media (max-width: 400px) {
  .loopie-bot-window {
    width: 100vw;
    height: 100vh;
    bottom: 0;
    right: 0;
    border-radius: 0;
  }
}
