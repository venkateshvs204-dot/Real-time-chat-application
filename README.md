# Real-time-chat-application
import React, { useState } from 'react';
import './App.css';

export default function ChatApp() {
  // Mock State representing structural active chat windows
  const [activeRoom, setActiveRoom] = useState('group-1');

  return (
    <div className="chat-app">
      {/* Sidebar: One-on-One & Group Targets */}
      <aside className="sidebar">
        <div className="user-profile-bar">
          <div className="avatar" style={{width: '32px', height: '32px', fontSize: '12px'}}>ME</div>
          <span style={{fontWeight: '600', fontSize: '14px'}}>Alex Rivera</span>
          <button style={{background: 'none', border: 'none', color: '#8a99ad', cursor: 'pointer'}}>⚙️</button>
        </div>
        
        <div className="rooms-list">
          {/* Group Chat Item Structure */}
          <div 
            className={`room-item ${activeRoom === 'group-1' ? 'active' : ''}`}
            onClick={() => setActiveRoom('group-1')}
          >
            <div className="avatar-container">
              <div className="avatar">👥</div>
            </div>
            <div className="room-info">
              <h4>Dev Team Sync (Group)</h4>
              <p>Sarah: Just pushed the latest security patches...</p>
            </div>
          </div>

          {/* Direct 1-on-1 Chat Item Structure (with Online Status) */}
          <div 
            className={`room-item ${activeRoom === 'user-2' ? 'active' : ''}`}
            onClick={() => setActiveRoom('user-2')}
          >
            <div className="avatar-container">
              <div className="avatar">JD</div>
              <span className="status-indicator online"></span> {/* Online Status */}
            </div>
            <div className="room-info">
              <h4>Jane Doe (1-on-1)</h4>
              <p>Are we still meeting today?</p>
            </div>
          </div>
        </div>
      </aside>

      {/* Main Chat Panel View */}
      <main className="chat-window">
        <header className="chat-header">
          <div className="avatar" style={{marginRight: '12px'}}>
            {activeRoom === 'group-1' ? '👥' : 'JD'}
          </div>
          <div>
            <h3 style={{margin: 0, fontSize: '16px'}}>
              {activeRoom === 'group-1' ? 'Dev Team Sync' : 'Jane Doe'}
            </h3>
            <span style={{fontSize: '11px', color: '#2ecc71'}}>
              {activeRoom === 'group-1' ? '5 members online' : 'online'}
            </span>
          </div>
        </header>

        {/* Dynamic Messaging Feed Container */}
        <div className="messages-container">
          {/* Encryption Indicator */}
          <div className="encryption-badge">
            🔒 Messages are end-to-end encrypted. No one outside of this chat can read them.
          </div>

          {/* Received Message Example Block */}
          <div className="message-row received">
            {activeRoom === 'group-1' && <span className="sender-name">Sarah Connor</span>}
            <div className="message-bubble">
              Hey everyone! Did we finalize the schema layout for the MongoDB connection?
            </div>
            <div className="message-meta">
              <span>10:42 PM</span>
            </div>
          </div>

          {/* Sent Message Example Block (With Read Receipt Statuses) */}
          <div className="message-row sent">
            <div className="message-bubble">
              Yes, I updated the model rules. Messages are passing securely through our WebSockets layer.
            </div>
            <div className="message-meta">
              <span>10:45 PM</span>
              {/* Read Receipt ticks element: add 'read' class for blue double tick */}
              <span className="receipt-tick read">✓✓</span> 
            </div>
          </div>
        </div>

        {/* Message Inputs Box Area */}
        <footer className="chat-input-area">
          <form className="input-form" onSubmit={(e) => e.preventDefault()}>
            <input type="text" placeholder="Type an encrypted message..." />
            <button type="submit" className="send-btn">➔</button>
          </form>
        </footer>
      </main>
    </div>
  );
}
