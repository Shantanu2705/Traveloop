import React, { useState, useEffect, useRef } from 'react';
import './LoopieBot.css';

const LoopieBot = () => {
  const [isOpen, setIsOpen] = useState(false);
  const [messages, setMessages] = useState([]);
  const [inputText, setInputText] = useState('');
  const messagesEndRef = useRef(null);

  const supportNumber = "+91 9732395264";

  const toggleBot = () => setIsOpen(!isOpen);

  useEffect(() => {
    if (isOpen && messages.length === 0) {
      // Initial greeting
      addBotMessage("Namaste! 🙏 I am Loopie, your personal Traveloop AI guide. Ready to explore the world?", [
        { label: "Plan a Trip in India 🇮🇳", action: "plan_india" },
        { label: "International Trip 🌍", action: "plan_intl" },
        { label: "Contact Support 📞", action: "support" }
      ]);
    }
  }, [isOpen]);

  useEffect(() => {
    scrollToBottom();
  }, [messages]);

  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
  };

  const addBotMessage = (text, options = null, images = null) => {
    setMessages(prev => [...prev, { sender: 'bot', text, options, images }]);
  };

  const addUserMessage = (text) => {
    setMessages(prev => [...prev, { sender: 'user', text }]);
  };

  const handleOptionClick = (option) => {
    addUserMessage(option.label);
    processBotLogic(option.action);
  };

  const processBotLogic = (action) => {
    setTimeout(() => {
      switch (action) {
        case 'plan_india':
          addBotMessage("Great choice! India has incredible diversity. Which region are you interested in?", [
            { label: "North (Mountains & Heritage) 🏔️", action: "india_north" },
            { label: "South (Beaches & Backwaters) 🏖️", action: "india_south" },
            { label: "West (Deserts & Culture) 🐪", action: "india_west" },
            { label: "East (Nature & Hills) 🌿", action: "india_east" }
          ]);
          break;
        case 'india_north':
          addBotMessage("North India is stunning! Here are a couple of popular destinations:", [
            { label: "Plan for Jaipur", action: "plan_jaipur" },
            { label: "Plan for Manali", action: "plan_manali" }
          ], [
            { url: "https://images.unsplash.com/photo-1477587458883-47145ed94245?auto=format&fit=crop&w=400&q=80", title: "Jaipur, Rajasthan" },
            { url: "https://images.unsplash.com/photo-1626621341517-bbf3d9990a23?auto=format&fit=crop&w=400&q=80", title: "Manali, Himachal Pradesh" }
          ]);
          break;
        case 'india_south':
          addBotMessage("South India offers a serene experience! Take a look:", [
            { label: "Plan for Kerala", action: "plan_kerala" },
            { label: "Plan for Goa", action: "plan_goa" }
          ], [
            { url: "https://images.unsplash.com/photo-1602216056096-3b40cc0c9944?auto=format&fit=crop&w=400&q=80", title: "Backwaters, Kerala" },
            { url: "https://images.unsplash.com/photo-1512343879784-a960bf40e7f2?auto=format&fit=crop&w=400&q=80", title: "Beaches, Goa" }
          ]);
          break;
        case 'india_west':
          addBotMessage("West India is vibrant and royal. Let me know if you want to proceed!", [
             { label: "Plan for Udaipur", action: "plan_udaipur" }
          ], [
             { url: "https://images.unsplash.com/photo-1615836245337-f839dffdbac3?auto=format&fit=crop&w=400&q=80", title: "Udaipur, Rajasthan" }
          ]);
          break;
        case 'india_east':
          addBotMessage("East India is filled with lush green landscapes!", [
             { label: "Plan for Darjeeling", action: "plan_darjeeling" }
          ], [
             { url: "https://images.unsplash.com/photo-1542359649-31e03cd4d909?auto=format&fit=crop&w=400&q=80", title: "Tea Gardens, Darjeeling" }
          ]);
          break;
        case 'plan_intl':
          addBotMessage("Exciting! We cover major international cities. Where to?", [
            { label: "Europe (Paris, Rome) 🗼", action: "intl_europe" },
            { label: "Asia (Dubai, Bali) 🌴", action: "intl_asia" }
          ]);
          break;
        case 'intl_europe':
          addBotMessage("Europe is a timeless classic.", null, [
            { url: "https://images.unsplash.com/photo-1502602881469-414757514111?auto=format&fit=crop&w=400&q=80", title: "Paris, France" }
          ]);
          break;
        case 'intl_asia':
          addBotMessage("Asia is exotic and luxurious.", null, [
            { url: "https://images.unsplash.com/photo-1512453979798-5ea266f8880c?auto=format&fit=crop&w=400&q=80", title: "Dubai, UAE" }
          ]);
          break;
        case 'support':
          addBotMessage(`For serious doubts or immediate assistance, please call our Traveloop Support Team directly at ${supportNumber}. We are available 24/7!`, [
            { label: "Go Back", action: "restart" }
          ]);
          break;
        case 'restart':
          addBotMessage("How else can I help you?", [
            { label: "Plan a Trip in India 🇮🇳", action: "plan_india" },
            { label: "International Trip 🌍", action: "plan_intl" },
            { label: "Contact Support 📞", action: "support" }
          ]);
          break;
        default:
          addBotMessage("I've saved your choice! A Traveloop agent will review your itinerary plan. Is there anything else you need?", [
             { label: "Contact Support 📞", action: "support" },
             { label: "Start Over 🔄", action: "restart" }
          ]);
          break;
      }
    }, 600);
  };

  const handleSend = (e) => {
    e.preventDefault();
    if (!inputText.trim()) return;
    
    addUserMessage(inputText);
    const lowerInput = inputText.toLowerCase();
    setInputText('');
    
    setTimeout(() => {
      if (lowerInput.includes('help') || lowerInput.includes('support') || lowerInput.includes('issue')) {
        processBotLogic('support');
      } else if (lowerInput.includes('india')) {
        processBotLogic('plan_india');
      } else {
        addBotMessage("I'm Loopie! While I am still learning custom requests, you can use the options below to plan your trip, or contact support for complex queries.", [
           { label: "Show Menu", action: "restart" },
           { label: "Contact Support", action: "support" }
        ]);
      }
    }, 800);
  };

  return (
    <div className="loopie-bot-container">
      {isOpen ? (
        <div className="loopie-bot-window">
          <div className="loopie-bot-header">
            <div className="header-info">
              <span className="bot-avatar">✈️</span>
              <div>
                <h4>Loopie AI</h4>
                <p>Traveloop Virtual Guide</p>
              </div>
            </div>
            <button className="close-bot" onClick={toggleBot}>&times;</button>
          </div>
          
          <div className="loopie-bot-messages">
            {messages.map((msg, index) => (
              <div key={index} className={`message-row ${msg.sender}`}>
                <div className={`message-bubble ${msg.sender}`}>
                  <p>{msg.text}</p>
                  
                  {msg.images && (
                    <div className="message-images">
                      {msg.images.map((img, i) => (
                        <div key={i} className="image-card">
                          <img src={img.url} alt={img.title} />
                          <span>{img.title}</span>
                        </div>
                      ))}
                    </div>
                  )}

                  {msg.options && (
                    <div className="message-options">
                      {msg.options.map((opt, i) => (
                        <button key={i} onClick={() => handleOptionClick(opt)}>
                          {opt.label}
                        </button>
                      ))}
                    </div>
                  )}
                </div>
              </div>
            ))}
            <div ref={messagesEndRef} />
          </div>
          
          <form className="loopie-bot-input" onSubmit={handleSend}>
            <input 
              type="text" 
              placeholder="Type your message..." 
              value={inputText}
              onChange={(e) => setInputText(e.target.value)}
            />
            <button type="submit">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
                <line x1="22" y1="2" x2="11" y2="13"></line>
                <polygon points="22 2 15 22 11 13 2 9 22 2"></polygon>
              </svg>
            </button>
          </form>
        </div>
      ) : (
        <button className="loopie-bot-launcher" onClick={toggleBot}>
          <span className="launcher-icon">💬</span>
        </button>
      )}
    </div>
  );
};

export default LoopieBot;
