<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Montessori Advanced Pairing</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background: #000;
            color: #e2e8f0;
            overscroll-behavior: none;
        }
        .container {
            max-width: 900px;
            height: 100vh;
            margin: 0 auto;
            background-color: #1a1a1a;
            padding: 2rem;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
            gap: 2rem;
            border-radius: 0;
            box-shadow: none;
            position: relative;
            z-index: 10;
        }
        @media (min-width: 768px) {
            .container {
                border-radius: 1rem;
                box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.5), 0 4px 6px -2px rgba(0, 0, 0, 0.4);
                height: auto;
                margin: 2rem auto;
            }
        }
        .row {
            padding: 1rem;
            background-color: #222;
            border-radius: 0.5rem;
            box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.2);
        }
        .note {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: linear-gradient(135deg, #FF6B6B, #F9D03F, #2ECC71, #3498DB, #9B59B6);
            color: white;
            font-size: 1.5rem;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.1s ease, box-shadow 0.2s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
        }
        .note:hover { transform: translateY(-2px); box-shadow: 0 6px 8px rgba(0, 0, 0, 0.5); }
        .note:active { transform: translateY(0); box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3); }
        .note.reference {
            background: #7F8C8D;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
        }
        .note.selected {
            border: 4px solid #1d4ed8;
            background: linear-gradient(135deg, #1d4ed8, #3b82f6);
            box-shadow: 0 4px 10px rgba(29, 78, 216, 0.7);
        }
        .note.correct {
            background: #27ae60;
            animation: pulse-green 1s infinite;
        }
        .note.wrong {
            background: #e74c3c;
            animation: shake 0.5s;
        }
        @keyframes pulse-green {
            0%, 100% { box-shadow: 0 0 0 0 rgba(46, 204, 113, 0.7); }
            50% { box-shadow: 0 0 0 10px rgba(46, 204, 113, 0); }
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-5px); }
            40%, 80% { transform: translateX(5px); }
        }
    </style>
</head>
<body class="p-4 sm:p-8 relative">
    <div class="container md:flex-row md:items-start md:space-x-8">
        <div class="flex-1 flex flex-col space-y-4">
            <h1 class="text-3xl sm:text-4xl font-extrabold text-blue-400 md:hidden">Advanced Pairing</h1>
            
            <div class="row">
                <h2 class="text-xl font-semibold mb-4 text-blue-300">1. Select an Instrument</h2>
                <div class="flex flex-wrap gap-4 justify-center">
                    <button data-instrument="piano" class="px-6 py-2 rounded-full border border-blue-400 text-blue-300 bg-gray-800 hover:bg-gray-700 transition-colors instrument-btn active:bg-gray-600">Piano</button>
                    <button data-instrument="guitar" class="px-6 py-2 rounded-full border border-blue-400 text-blue-300 bg-gray-800 hover:bg-gray-700 transition-colors instrument-btn active:bg-gray-600">Electric Guitar</button>
                    <button data-instrument="flute" class="px-6 py-2 rounded-full border border-blue-400 text-blue-300 bg-gray-800 hover:bg-gray-700 transition-colors instrument-btn active:bg-gray-600">Flute</button>
                    <button data-instrument="violin" class="px-6 py-2 rounded-full border border-blue-400 text-blue-300 bg-gray-800 hover:bg-gray-700 transition-colors instrument-btn active:bg-gray-600">Violin</button>
                    <button data-instrument="drums" class="px-6 py-2 rounded-full border border-blue-400 text-blue-300 bg-gray-800 hover:bg-gray-700 transition-colors instrument-btn active:bg-gray-600">Drums</button>
                    <button data-instrument="tabla" class="px-6 py-2 rounded-full border border-blue-400 text-blue-300 bg-gray-800 hover:bg-gray-700 transition-colors instrument-btn active:bg-gray-600">Tabla</button>
                </div>
            </div>

            <div class="row flex flex-col md:flex-row justify-between items-center md:space-x-4">
                <div class="flex-1 w-full mb-4 md:mb-0">
                    <h2 class="text-xl font-semibold mb-2 text-blue-300">2. Select a Scale</h2>
                    <select id="scale-select" class="w-full p-2 border border-gray-600 rounded-md bg-gray-800 text-white">
                        <option value="C">C Major</option>
                        <option value="G">G Major</option>
                        <option value="D">D Major</option>
                        <option value="A">A Major</option>
                        <option value="E">E Major</option>
                        <option value="B">B Major</option>
                    </select>
                </div>
                <div class="flex-1 w-full">
                    <h2 class="text-xl font-semibold mb-2 text-blue-300">3. Select Tones</h2>
                    <select id="tone-select" class="w-full p-2 border border-gray-600 rounded-md bg-gray-800 text-white">
                        <option value="all">All Tones</option>
                        <option value="whole">Whole Tones Only</option>
                    </select>
                </div>
            </div>

            <div class="row">
                <h2 class="text-xl font-semibold mb-4 text-blue-300">4. Select a Reference Note</h2>
                <div id="reference-notes-container" class="flex flex-wrap gap-4 justify-center">
                    </div>
            </div>
        </div>

        <div class="flex-1 flex flex-col space-y-4">
            <h1 class="text-3xl sm:text-4xl font-extrabold text-center text-blue-400 hidden md:block">Advanced Pairing</h1>
            <div class="row flex-1 flex flex-col justify-center items-center">
                <h2 class="text-xl font-semibold mb-4 text-blue-300">5. The Challenge</h2>
                
                <div class="grid grid-cols-1 gap-8 items-center w-full">
                    <div class="flex flex-col items-center">
                        <p class="text-center font-bold text-xl mb-2 text-blue-200" id="reference-note-name"></p>
                        <div id="reference-note" class="note reference cursor-pointer">🎵</div>
                    </div>

                    <div class="flex flex-col items-center">
                        <h3 class="text-lg font-semibold mb-2 text-gray-400">The Full Scale</h3>
                        <div id="full-scale-display" class="flex justify-center gap-2 flex-wrap"></div>
                    </div>
                </div>
                
                <div class="flex flex-col items-center mt-8">
                    <h3 class="text-lg font-semibold mb-2 text-gray-400">Find the Match Below</h3>
                    <div id="pairing-notes-container" class="flex justify-center gap-4 flex-wrap"></div>
                </div>

                <div class="flex justify-center mt-8 space-x-4">
                    <button id="confirm-btn" class="bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-lg hover:bg-blue-700 transition-colors disabled:bg-gray-600 disabled:cursor-not-allowed">
                        Confirm Match
                    </button>
                    <button id="reset-btn" class="bg-gray-500 text-white font-semibold py-2 px-6 rounded-full shadow-lg hover:bg-gray-600 transition-colors">
                        New Round
                    </button>
                </div>
            </div>
        </div>

        <div id="message-modal" class="hidden fixed inset-0 bg-gray-900 bg-opacity-75 flex items-center justify-center p-4 z-50">
            <div class="bg-gray-800 rounded-lg p-6 w-full max-w-sm text-center shadow-2xl">
                <p id="modal-text" class="text-lg font-semibold text-white mb-4"></p>
                <button id="modal-close" class="bg-blue-600 text-white py-2 px-4 rounded-full font-semibold hover:bg-blue-700">Close</button>
            </div>
        </div>
    </div>

    <script>
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        let currentInstrument = 'piano';

        const noteFrequencies = {
            'C': 261.63, 'C#': 277.18, 'D': 293.66, 'D#': 311.13, 'E': 329.63, 'F': 349.23,
            'F#': 369.99, 'G': 392.00, 'G#': 415.30, 'A': 440.00, 'A#': 466.16, 'B': 493.88
        };
        const allNotes = Object.keys(noteFrequencies);

        const scales = {
            'C': ['C', 'D', 'E', 'F', 'G', 'A', 'B'],
            'G': ['G', 'A', 'B', 'C', 'D', 'E', 'F#'],
            'D': ['D', 'E', 'F#', 'G', 'A', 'B', 'C#'],
            'A': ['A', 'B', 'C#', 'D', 'E', 'F#', 'G#'],
            'E': ['E', 'F#', 'G#', 'A', 'B', 'C#', 'D#'],
            'B': ['B', 'C#', 'D#', 'E', 'F#', 'G#', 'A#']
        };

        let referenceNote = '';
        let selectedNote = null;
        let availableNotes = [];
        let matchedNotes = [];

        // UI elements
        const instrumentBtns = document.querySelectorAll('.instrument-btn');
        const scaleSelect = document.getElementById('scale-select');
        const toneSelect = document.getElementById('tone-select');
        const referenceNotesContainer = document.getElementById('reference-notes-container');
        const referenceNoteEl = document.getElementById('reference-note');
        const referenceNoteNameEl = document.getElementById('reference-note-name');
        const fullScaleDisplayEl = document.getElementById('full-scale-display');
        const pairingNotesContainer = document.getElementById('pairing-notes-container');
        const confirmBtn = document.getElementById('confirm-btn');
        const resetBtn = document.getElementById('reset-btn');

        // Functions
        function playNote(frequency, instrument, duration = 0.5) {
            if (!audioContext) return;
            const now = audioContext.currentTime;

            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            const vibrato = audioContext.createOscillator();
            const vibratoGain = audioContext.createGain();
            const noise = audioContext.createBufferSource();
            const noiseGain = audioContext.createGain();
            const filter = audioContext.createBiquadFilter();

            gainNode.gain.setValueAtTime(0, now);
            gainNode.gain.linearRampToValueAtTime(0.5, now + 0.01);

            switch (instrument) {
                case 'piano':
                    oscillator.type = 'sine';
                    gainNode.gain.exponentialRampToValueAtTime(0.001, now + duration);
                    break;
                case 'guitar':
                    oscillator.type = 'sawtooth';
                    vibrato.type = 'sine';
                    vibrato.frequency.setValueAtTime(5, now);
                    vibratoGain.gain.setValueAtTime(frequency / 20, now);
                    vibrato.connect(vibratoGain);
                    vibratoGain.connect(oscillator.frequency);
                    gainNode.gain.exponentialRampToValueAtTime(0.001, now + duration);
                    vibrato.start(now);
                    break;
                case 'flute':
                    oscillator.type = 'sine';
                    vibrato.type = 'sine';
                    vibrato.frequency.setValueAtTime(3, now);
                    vibratoGain.gain.setValueAtTime(frequency / 40, now);
                    vibrato.connect(vibratoGain);
                    vibratoGain.connect(oscillator.frequency);
                    gainNode.gain.linearRampToValueAtTime(0.3, now + 0.2);
                    gainNode.gain.linearRampToValueAtTime(0, now + duration);
                    vibrato.start(now);
                    break;
                case 'violin':
                    oscillator.type = 'sawtooth';
                    vibrato.type = 'sine';
                    vibrato.frequency.setValueAtTime(6, now);
                    vibratoGain.gain.setValueAtTime(frequency / 20, now);
                    vibrato.connect(vibratoGain);
                    vibratoGain.connect(oscillator.frequency);
                    gainNode.gain.linearRampToValueAtTime(0.6, now + 0.5);
                    gainNode.gain.linearRampToValueAtTime(0, now + duration);
                    vibrato.start(now);
                    break;
                case 'drums':
                    oscillator.type = 'sine';
                    gainNode.gain.linearRampToValueAtTime(0.001, now + 0.05);
                    break;
                case 'tabla':
                    oscillator.type = 'sine';
                    const bufferSize = audioContext.sampleRate * 2;
                    const buffer = audioContext.createBuffer(1, bufferSize, audioContext.sampleRate);
                    const output = buffer.getChannelData(0);
                    for (let i = 0; i < bufferSize; i++) {
                        output[i] = Math.random() * 2 - 1;
                    }
                    noise.buffer = buffer;
                    noise.loop = true;
                    noiseGain.gain.setValueAtTime(0, now);
                    noiseGain.gain.linearRampToValueAtTime(0.1, now + 0.01);
                    noiseGain.gain.linearRampToValueAtTime(0.001, now + duration);
                    noise.connect(noiseGain);
                    noiseGain.connect(audioContext.destination);
                    noise.start(now);

                    filter.type = 'lowpass';
                    filter.frequency.setValueAtTime(1000, now);
                    filter.Q.setValueAtTime(1, now);
                    oscillator.connect(filter);
                    filter.connect(gainNode);

                    gainNode.gain.linearRampToValueAtTime(0.5, now + 0.01);
                    gainNode.gain.linearRampToValueAtTime(0, now + duration);
                    break;
            }

            oscillator.frequency.setValueAtTime(frequency, now);
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            oscillator.start(now);
            oscillator.stop(now + duration);
        }

        function showMessage(text) {
            const modal = document.getElementById('message-modal');
            const modalText = document.getElementById('modal-text');
            modalText.textContent = text;
            modal.classList.remove('hidden');
        }

        document.getElementById('modal-close').addEventListener('click', () => {
            document.getElementById('message-modal').classList.add('hidden');
        });

        function getFilteredScale() {
            const selectedScaleKey = scaleSelect.value;
            const selectedTones = toneSelect.value;
            let currentScale = scales[selectedScaleKey];

            if (selectedTones === 'whole') {
                const wholeTones = [];
                const notes = currentScale;
                const intervals = [2, 2, 1, 2, 2, 2, 1];
                let cumulativeInterval = 0;

                for (let i = 0; i < intervals.length; i++) {
                    const nextNoteIndex = allNotes.indexOf(notes[0]) + cumulativeInterval;
                    if(nextNoteIndex < allNotes.length) {
                       wholeTones.push(allNotes[nextNoteIndex]);
                    }
                    cumulativeInterval += intervals[i];
                }
                currentScale = wholeTones.filter(note => notes.includes(note));
            }
            return currentScale;
        }

        function setupGame() {
            const currentScale = getFilteredScale();
            matchedNotes = [];
            
            // Set up reference notes for selection
            referenceNotesContainer.innerHTML = '';
            currentScale.forEach(note => {
                const container = document.createElement('div');
                container.className = 'flex flex-col items-center gap-1';
                
                const noteName = document.createElement('span');
                noteName.textContent = note;
                noteName.className = 'text-sm font-semibold text-gray-400';

                const noteEl = document.createElement('div');
                noteEl.className = 'note cursor-pointer';
                noteEl.textContent = '🎵';
                noteEl.dataset.note = note;
                noteEl.onclick = () => selectReferenceNote(note);

                container.appendChild(noteName);
                container.appendChild(noteEl);
                referenceNotesContainer.appendChild(container);
            });

            // Set up pairing notes
            availableNotes = [...currentScale].sort(() => Math.random() - 0.5);
            pairingNotesContainer.innerHTML = '';
            
            selectedNote = null;
            confirmBtn.disabled = true;

            availableNotes.forEach(note => {
                const noteEl = document.createElement('div');
                noteEl.className = 'note';
                noteEl.textContent = '🎵';
                noteEl.dataset.note = note;
                noteEl.onclick = (e) => {
                    playNote(noteFrequencies[note], currentInstrument);
                    if (!matchedNotes.includes(e.currentTarget.dataset.note)) {
                        if (selectedNote) {
                            selectedNote.classList.remove('selected');
                        }
                        selectedNote = e.currentTarget;
                        selectedNote.classList.add('selected');
                        confirmBtn.disabled = false;
                    }
                };
                pairingNotesContainer.appendChild(noteEl);
            });

            // Display full scale
            fullScaleDisplayEl.innerHTML = '';
            currentScale.forEach(note => {
                const noteEl = document.createElement('div');
                noteEl.className = 'flex items-center justify-center w-8 h-8 rounded-full bg-gray-700 text-sm font-bold';
                noteEl.textContent = note;
                fullScaleDisplayEl.appendChild(noteEl);
            });
        }

        function selectReferenceNote(note) {
            referenceNote = note;
            referenceNoteNameEl.textContent = '';
            referenceNoteEl.onclick = () => playNote(noteFrequencies[note], currentInstrument);
            playNote(noteFrequencies[note], currentInstrument);

            // Highlight the selected reference note
            document.querySelectorAll('#reference-notes-container .note').forEach(el => {
                el.classList.remove('bg-blue-600', 'text-white');
                el.classList.add('bg-gray-700');
            });
            const selectedRefNoteEl = document.querySelector(`#reference-notes-container .note[data-note="${note}"]`);
            selectedRefNoteEl.classList.add('bg-blue-600', 'text-white');
            selectedRefNoteEl.classList.remove('bg-gray-700');
        }

        // Event Listeners
        instrumentBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                currentInstrument = btn.dataset.instrument;
                instrumentBtns.forEach(b => b.classList.remove('bg-gray-600', 'active'));
                btn.classList.add('bg-gray-600', 'active');
            });
        });

        scaleSelect.addEventListener('change', setupGame);
        toneSelect.addEventListener('change', setupGame);

        confirmBtn.addEventListener('click', () => {
            if (!selectedNote) return;
            if (selectedNote.dataset.note === referenceNote) {
                selectedNote.classList.add('correct');
                showMessage("You found the match! Great job!");
                confirmBtn.disabled = true;
                matchedNotes.push(selectedNote.dataset.note);
                selectedNote.classList.remove('selected');
                selectedNote = null;
            } else {
                selectedNote.classList.add('wrong');
                showMessage("That's not the correct note. Try again!");
                setTimeout(() => {
                    selectedNote.classList.remove('wrong');
                }, 500);
            }
        });

        resetBtn.addEventListener('click', () => {
            setupGame();
            showMessage("All notes have been reset. Please select a new reference note.");
        });
        
        // Initial setup
        setupGame();
    </script>
</body>
</html>
```eof
