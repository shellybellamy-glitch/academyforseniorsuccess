import React, { useState, useEffect, useRef } from 'react';
import { 
  MousePointer2, Hand, CircleDot, Mouse, ArrowDownUp, 
  CheckCircle2, RotateCcw, ChevronRight, ChevronLeft, Info,
  HandMetal, Sparkles, MessageSquare, Brain
} from 'lucide-react';
import { initializeApp } from 'firebase/app';
import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from 'firebase/auth';

const App = () => {
  // --- State ---
  const [currentStep, setCurrentStep] = useState(0);
  const [practiceState, setPracticeState] = useState('instruction');
  const [score, setScore] = useState(0);
  const [targetPos, setTargetPos] = useState({ x: 50, y: 50 });
  const [feedback, setFeedback] = useState("");
  const [showRightMenu, setShowRightMenu] = useState(false);
  const [aiLoading, setAiLoading] = useState(false);
  const [aiResponse, setAiResponse] = useState("");
  const [user, setUser] = useState(null);

  // Drag and Drop State
  const [isDragging, setIsDragging] = useState(false);
  const [dragPos, setDragPos] = useState({ x: 20, y: 50 });

  // Gemini API Key (handled by environment)
  const apiKey = "";

  const lessons = [
    {
      id: "moving",
      title: "1. Moving the Mouse",
      instruction: "The mouse is your 'digital finger'. Move it around to point at things on the screen.",
      icon: <Hand className="w-12 h-12 text-blue-500" />,
      action: "Move your mouse to follow the blue circle.",
      type: "move"
    },
    {
      id: "clicking",
      title: "2. The Left Click",
      instruction: "The Left Button is your 'Select' button. Use it to press buttons and open items.",
      icon: <MousePointer2 className="w-12 h-12 text-green-500" />,
      action: "Click the red buttons as they appear.",
      type: "click"
    },
    {
      id: "double",
      title: "3. The Double-Click",
      instruction: "Sometimes you need to click TWICE very quickly. This is often used to open folders or start programs.",
      icon: <Mouse className="w-12 h-12 text-yellow-500" />,
      action: "Click the folder TWICE quickly to open it.",
      type: "double-click"
    },
    {
      id: "drag",
      title: "4. Drag and Drop",
      instruction: "To move things, press and HOLD the left button, move the mouse, then LET GO.",
      icon: <HandMetal className="w-12 h-12 text-red-500" />,
      action: "Hold the block and move it into the 'Goal' area.",
      type: "drag-drop"
    },
    {
      id: "right",
      title: "5. The Right Click",
      instruction: "The Right Button opens 'Options'. It’s like asking the computer 'What can I do with this?'",
      icon: <CircleDot className="w-12 h-12 text-purple-500" />,
      action: "Right-click inside the box to see the menu.",
      type: "right-click"
    },
    {
      id: "scroll",
      title: "6. Scrolling",
      instruction: "Use the little wheel to move pages up and down without moving your whole hand.",
      icon: <ArrowDownUp className="w-12 h-12 text-orange-500" />,
      action: "Scroll to the bottom of the list.",
      type: "scroll"
    }
  ];

  // --- Gemini API Integration ---
  const callGemini = async (prompt, systemPrompt = "You are a patient, friendly technology tutor for seniors.") => {
    setAiLoading(true);
    setAiResponse("");
    
    const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
    
    const payload = {
      contents: [{ parts: [{ text: prompt }] }],
      systemInstruction: { parts: [{ text: systemPrompt }] }
    };

    let retries = 0;
    const maxRetries = 5;
    
    while (retries < maxRetries) {
      try {
        const response = await fetch(url, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });
        
        if (!response.ok) throw new Error('API Error');
        
        const data = await response.json();
        const text = data.candidates?.[0]?.content?.parts?.[0]?.text;
        setAiResponse(text);
        setAiLoading(false);
        return;
      } catch (err) {
        retries++;
        await new Promise(res => setTimeout(res, Math.pow(2, retries) * 1000));
      }
    }
    setAiResponse("I'm sorry, I'm having trouble connecting right now. Please try again in a moment.");
    setAiLoading(false);
  };

  const getSmartHelp = () => {
    const lesson = lessons[currentStep];
    const prompt = `The user is a senior learning how to use a computer mouse. They are currently on the lesson: "${lesson.title}". The specific task is: "${lesson.action}". 
    
    Please provide 2-3 sentences of very simple, encouraging advice on how to perform this specific mouse action. Use analogies where helpful (like comparing the mouse to a physical tool). Keep it short and easy to read.`;
    
    callGemini(prompt);
  };

  const generateSmartQuiz = () => {
    const prompt = `The user has finished the Mouse Academy course. They learned: Moving, Clicking, Double-Clicking, Dragging, Right-Clicking, and Scrolling.
    
    Generate one encouraging "Final Quiz" question that asks them to identify which mouse button or action they would use for a real-world scenario (e.g., 'If you want to move a file from one folder to another, what action do you use?'). 
    
    Structure the response as: 
    QUESTION: [The question]
    ANSWER: [The correct action]
    EXPLANATION: [A short encouraging explanation why]`;
    
    callGemini(prompt, "You are a celebratory graduation host for a technology class.");
  };

  // --- Navigation & Gameplay ---
  const nextStep = () => {
    if (currentStep < lessons.length - 1) {
      setCurrentStep(currentStep + 1);
      setPracticeState('instruction');
      setScore(0);
      setFeedback("");
      setAiResponse("");
    } else {
      setPracticeState('graduation');
    }
  };

  const startPractice = () => {
    setPracticeState('practice');
    setScore(0);
    setDragPos({ x: 20, y: 50 });
    spawnTarget();
  };

  const spawnTarget = () => {
    setTargetPos({ x: Math.random() * 70 + 15, y: Math.random() * 70 + 15 });
  };

  const handleMoveComplete = () => {
    setFeedback("Great movement!");
    setTimeout(nextStep, 1000);
  };

  // --- Auth & Setup ---
  useEffect(() => {
    const firebaseConfig = JSON.parse(window.__firebase_config || '{}');
    if (firebaseConfig.apiKey) {
      const app = initializeApp(firebaseConfig);
      const auth = getAuth(app);
      const initAuth = async () => {
        if (typeof window.__initial_auth_token !== 'undefined' && window.__initial_auth_token) {
          await signInWithCustomToken(auth, window.__initial_auth_token);
        } else {
          await signInAnonymously(auth);
        }
      };
      initAuth();
      return onAuthStateChanged(auth, setUser);
    }
  }, []);

  return (
    <div className="min-h-screen bg-slate-100 p-4 font-sans flex flex-col items-center">
      <header className="mb-6 text-center">
        <h1 className="text-3xl font-bold text-blue-800 flex items-center justify-center gap-2">
          <Mouse className="w-8 h-8" /> Senior Mouse Academy
        </h1>
        <p className="text-slate-500 italic">No rush, take your time.</p>
      </header>

      <div className="max-w-6xl w-full bg-white rounded-3xl shadow-2xl flex flex-col lg:flex-row min-h-[600px] border-4 border-white overflow-hidden">
        
        {/* Progress Sidebar */}
        <div className="w-full lg:w-72 bg-slate-50 p-6 border-r flex flex-col">
          <div className="space-y-2 mb-8">
            <h3 className="text-xs font-bold text-slate-400 uppercase tracking-widest mb-4">Your Progress</h3>
            {lessons.map((l, i) => (
              <div key={i} className={`p-3 rounded-xl flex items-center gap-3 transition-colors ${i === currentStep ? 'bg-blue-600 text-white shadow-md' : 'text-slate-400'}`}>
                {i < currentStep ? <CheckCircle2 className="w-5 h-5 text-green-400" /> : <span className="w-5 text-center font-mono">{i+1}</span>}
                <span className="text-sm font-bold">{l.title.split('. ')[1]}</span>
              </div>
            ))}
          </div>

          <div className="mt-auto bg-blue-50 p-4 rounded-2xl border border-blue-100">
            <h4 className="font-bold text-blue-800 text-sm flex items-center gap-1 mb-1">
              <Sparkles className="w-4 h-4" /> AI Smart Tutor
            </h4>
            <p className="text-xs text-blue-600 leading-relaxed mb-3">
              Need a better explanation? Ask our ✨ Smart Tutor for help.
            </p>
            <button 
              onClick={getSmartHelp}
              className="w-full py-2 bg-blue-100 hover:bg-blue-200 text-blue-800 rounded-lg text-xs font-bold transition flex items-center justify-center gap-2"
            >
              ✨ Help me with this!
            </button>
          </div>
        </div>

        {/* Practice Area */}
        <div className="flex-1 p-8 flex flex-col items-center justify-center relative">
          
          {/* AI Response Overlay */}
          {aiLoading && (
            <div className="absolute inset-0 bg-white/80 backdrop-blur-sm z-50 flex flex-col items-center justify-center">
              <div className="animate-spin rounded-full h-12 w-12 border-b-2 border-blue-600 mb-4"></div>
              <p className="text-blue-800 font-bold">✨ AI Tutor is thinking...</p>
            </div>
          )}

          {aiResponse && practiceState !== 'graduation' && (
            <div className="mb-6 p-4 bg-yellow-50 border-l-4 border-yellow-400 rounded-r-xl max-w-lg w-full animate-in slide-in-from-top duration-300">
              <div className="flex justify-between items-start mb-2">
                <span className="text-xs font-bold text-yellow-800 flex items-center gap-1 uppercase tracking-wider">
                  <Sparkles className="w-3 h-3" /> Smart Advice
                </span>
                <button onClick={() => setAiResponse("")} className="text-yellow-800 hover:text-black font-bold">✕</button>
              </div>
              <p className="text-slate-800 text-base leading-relaxed italic">"{aiResponse}"</p>
            </div>
          )}

          {practiceState === 'instruction' && (
            <div className="text-center animate-in fade-in zoom-in">
              <div className="flex justify-center mb-6">{lessons[currentStep].icon}</div>
              <h2 className="text-3xl font-bold mb-4">{lessons[currentStep].title}</h2>
              <p className="text-xl text-slate-700 mb-8 max-w-md">{lessons[currentStep].instruction}</p>
              <button onClick={startPractice} className="bg-blue-600 text-white text-xl px-12 py-4 rounded-full font-bold shadow-lg hover:bg-blue-700 transition transform active:scale-95">
                Let's Try It
              </button>
            </div>
          )}

          {practiceState === 'practice' && (
            <div className="w-full h-full flex flex-col">
              <div className="text-center font-bold text-blue-600 bg-blue-50 py-3 rounded-t-2xl border-x border-t border-blue-100 flex items-center justify-center gap-2">
                {lessons[currentStep].action}
              </div>
              <div className="relative flex-1 bg-slate-50 border-2 border-dashed border-slate-200 rounded-b-2xl overflow-hidden min-h-[350px]">
                
                {lessons[currentStep].type === "move" && (
                  <div className="w-full h-full relative" onMouseMove={(e) => {
                    const rect = e.currentTarget.getBoundingClientRect();
                    const x = ((e.clientX - rect.left) / rect.width) * 100;
                    const y = ((e.clientY - rect.top) / rect.height) * 100;
                    const dist = Math.sqrt(Math.pow(x - targetPos.x, 2) + Math.pow(y - targetPos.y, 2));
                    if (dist < 5) handleMoveComplete();
                  }}>
                    <div 
                      className="absolute w-20 h-20 bg-blue-400/30 rounded-full border-4 border-blue-500 flex items-center justify-center animate-pulse"
                      style={{ left: `${targetPos.x}%`, top: `${targetPos.y}%`, transform: 'translate(-50%, -50%)' }}
                    >
                      <div className="w-4 h-4 bg-blue-600 rounded-full" />
                    </div>
                  </div>
                )}

                {lessons[currentStep].type === "click" && (
                   <button 
                    onClick={() => { setScore(s => s+1); if(score >= 2) { setFeedback("Great!"); setTimeout(nextStep, 1500); } else spawnTarget(); }}
                    className="absolute w-20 h-20 bg-red-500 rounded-full border-4 border-white shadow-xl transform active:scale-90 transition"
                    style={{ left: `${targetPos.x}%`, top: `${targetPos.y}%`, transform: 'translate(-50%, -50%)' }}
                  >
                    <span className="text-white font-black">CLICK</span>
                  </button>
                )}

                {lessons[currentStep].type === "double-click" && (
                  <div className="flex items-center justify-center h-full">
                    <button 
                      onDoubleClick={() => {
                        setFeedback("Perfect double-click!");
                        setTimeout(nextStep, 1500);
                      }}
                      className="bg-yellow-100 p-8 rounded-3xl border-4 border-yellow-400 transform transition active:scale-95 shadow-lg group hover:bg-yellow-200"
                    >
                      <div className="text-7xl mb-2">📂</div>
                      <p className="font-bold text-yellow-800">Double-Click Folder</p>
                    </button>
                  </div>
                )}

                {lessons[currentStep].type === "drag-drop" && (
                  <div className="w-full h-full relative" onMouseMove={(e) => {
                    if (isDragging) {
                      const rect = e.currentTarget.getBoundingClientRect();
                      setDragPos({
                        x: Math.max(5, Math.min(95, ((e.clientX - rect.left) / rect.width) * 100)),
                        y: Math.max(5, Math.min(95, ((e.clientY - rect.top) / rect.height) * 100))
                      });
                    }
                  }}>
                    <div className="absolute right-12 top-1/2 -translate-y-1/2 w-40 h-40 border-4 border-red-300 border-dotted rounded-3xl flex items-center justify-center text-red-300 font-bold bg-white/50 uppercase tracking-widest">Goal</div>
                    <div 
                      onMouseDown={() => setIsDragging(true)}
                      onMouseUp={() => {
                        setIsDragging(false);
                        if (dragPos.x > 75) {
                          setFeedback("Excellent drag and drop!");
                          setTimeout(nextStep, 1500);
                        }
                      }}
                      className="absolute w-24 h-24 bg-red-500 rounded-2xl cursor-grab active:cursor-grabbing flex items-center justify-center shadow-2xl border-4 border-white z-10"
                      style={{ left: `${dragPos.x}%`, top: `${dragPos.y}%`, transform: 'translate(-50%, -50%)' }}
                    >
                      <HandMetal className="text-white w-10 h-10" />
                    </div>
                  </div>
                )}

                {lessons[currentStep].type === "right-click" && (
                  <div 
                    onContextMenu={(e) => { e.preventDefault(); setShowRightMenu(true); setFeedback("Menu opened!"); setTimeout(nextStep, 2000); }}
                    className="w-full h-full flex items-center justify-center p-10"
                  >
                    <div className="bg-purple-50 w-full h-full rounded-2xl border-2 border-purple-200 flex flex-col items-center justify-center border-dashed">
                       <p className="text-purple-700 font-bold text-xl mb-4 text-center">Right-click anywhere in this light purple area</p>
                       <CircleDot className="text-purple-300 w-24 h-24 animate-pulse" />
                       {showRightMenu && (
                         <div className="absolute bg-white shadow-2xl rounded-lg border border-slate-200 p-2 min-w-[150px] animate-in slide-in-from-top-4">
                           <div className="p-2 hover:bg-blue-50 rounded text-sm font-medium border-b border-slate-100">Open Folder</div>
                           <div className="p-2 hover:bg-blue-50 rounded text-sm font-medium">Copy Item</div>
                           <div className="p-2 hover:bg-blue-50 rounded text-sm font-medium">Delete Item</div>
                         </div>
                       )}
                    </div>
                  </div>
                )}

                {lessons[currentStep].type === "scroll" && (
                  <div className="w-full h-full overflow-y-auto bg-gradient-to-b from-white to-slate-200 p-8 custom-scrollbar">
                    <p className="text-2xl font-bold text-slate-400 mb-4 animate-bounce">Scroll down ↓</p>
                    {[...Array(40)].map((_, i) => (
                      <div key={i} className="py-4 border-b border-slate-200 text-slate-300 font-mono">
                        --- Section {i + 1} ---
                      </div>
                    ))}
                    <button 
                      onClick={nextStep}
                      className="mt-8 mb-40 w-full bg-orange-600 text-white py-10 rounded-3xl text-3xl font-black shadow-xl hover:bg-orange-700 transition"
                    >
                      YOU MADE IT! FINISH
                    </button>
                  </div>
                )}
              </div>
              {feedback && <div className="absolute bottom-12 left-1/2 -translate-x-1/2 text-3xl font-black text-green-600 drop-shadow-sm animate-bounce">{feedback}</div>}
            </div>
          )}

          {practiceState === 'graduation' && (
            <div className="text-center py-12 max-w-lg animate-in zoom-in duration-500">
              <div className="text-8xl mb-6">🏆</div>
              <h2 className="text-4xl font-black text-blue-900 mb-4">You are a Mouse Master!</h2>
              <p className="text-xl text-slate-600 mb-8">You have successfully mastered every mouse action needed to navigate a modern computer.</p>
              
              {aiResponse ? (
                <div className="mb-8 p-6 bg-blue-50 border-2 border-blue-200 rounded-3xl text-left shadow-inner">
                  <h4 className="font-bold text-blue-800 mb-2 flex items-center gap-2">
                    <Brain className="w-5 h-5" /> ✨ Final Graduation Question:
                  </h4>
                  <p className="text-slate-800 mb-4 font-medium leading-relaxed">{aiResponse.split('ANSWER:')[0].replace('QUESTION:', '').trim()}</p>
                  <details className="cursor-pointer group">
                    <summary className="text-blue-600 font-bold hover:underline list-none flex items-center gap-2">
                      <span className="bg-blue-600 text-white text-[10px] px-2 py-1 rounded-full">CHECK ANSWER</span>
                    </summary>
                    <div className="mt-4 p-4 bg-white rounded-xl border border-blue-100 animate-in slide-in-from-top-2">
                      <p className="text-green-700 font-bold mb-1">Correct Answer:</p>
                      <p className="text-slate-700">{aiResponse.split('ANSWER:')[1]?.split('EXPLANATION:')[0]?.trim()}</p>
                      <p className="text-slate-500 text-sm mt-2 italic">{aiResponse.split('EXPLANATION:')[1]?.trim()}</p>
                    </div>
                  </details>
                </div>
              ) : (
                <button 
                  onClick={generateSmartQuiz}
                  className="mb-8 bg-purple-600 text-white px-8 py-3 rounded-full font-bold shadow-lg hover:bg-purple-700 transition flex items-center gap-2 mx-auto"
                >
                  <Sparkles className="w-5 h-5" /> ✨ Quiz Me!
                </button>
              )}

              <button 
                onClick={() => {setCurrentStep(0); setPracticeState('instruction'); setAiResponse(""); }} 
                className="text-slate-400 hover:text-slate-600 font-bold underline decoration-2 underline-offset-4 transition"
              >
                Restart Course
              </button>
            </div>
          )}
        </div>
      </div>

      <footer className="max-w-6xl w-full mt-6 flex justify-between items-center px-4">
        <button 
          onClick={() => { setCurrentStep(s => Math.max(0, s-1)); setPracticeState('instruction'); setAiResponse(""); }}
          disabled={currentStep === 0}
          className="flex items-center gap-2 text-slate-500 font-bold disabled:opacity-0 transition hover:text-blue-600"
        >
          <ChevronLeft /> Previous Lesson
        </button>
        <div className="text-slate-400 font-bold text-sm tracking-widest bg-white px-4 py-1 rounded-full border border-slate-200 shadow-sm">
          UNIT {currentStep + 1} / {lessons.length}
        </div>
        <button 
          onClick={nextStep}
          disabled={practiceState === 'instruction' || practiceState === 'graduation'}
          className="flex items-center gap-2 text-blue-600 font-bold disabled:opacity-0 transition hover:text-blue-800"
        >
          Next Lesson <ChevronRight />
        </button>
      </footer>
    </div>
  );
};

export default App;