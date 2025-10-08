<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday Activities & Home Life</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Everyday Activities & Home Life</h1>
            <p>Test your knowledge of these English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>noise</h3>
                    <p><strong>Definition:</strong> A sound, especially one that is loud, unpleasant, or disturbing.</p>
                    <p><strong>Usage:</strong> Can refer to any unwanted or disruptive sound.</p>
                    <p class="example"><strong>Example:</strong> "The construction noise made it difficult to concentrate."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>hide</h3>
                    <p><strong>Definition:</strong> To put or keep out of sight; to conceal oneself or something.</p>
                    <p><strong>Usage:</strong> Can refer to physical concealment or keeping secrets.</p>
                    <p class="example"><strong>Example:</strong> "The children like to hide during games of hide and seek."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>get on (as salire sul treno)</h3>
                    <p><strong>Definition:</strong> To board or enter a vehicle, especially public transportation.</p>
                    <p><strong>Usage:</strong> Specifically used for entering trains, buses, planes, etc.</p>
                    <p class="example"><strong>Example:</strong> "We need to get on the train before it departs."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>playful</h3>
                    <p><strong>Definition:</strong> Fond of games and amusement; lighthearted and fun-loving.</p>
                    <p><strong>Usage:</strong> Describes people, animals, or behavior that is fun and energetic.</p>
                    <p class="example"><strong>Example:</strong> "The puppy was very playful and enjoyed chasing balls."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>how long does it take</h3>
                    <p><strong>Definition:</strong> A question asking about the duration or time required for something.</p>
                    <p><strong>Usage:</strong> Used to inquire about time needed for activities, travel, or tasks.</p>
                    <p class="example"><strong>Example:</strong> "How long does it take to get to the city center from here?"</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>house chores</h3>
                    <p><strong>Definition:</strong> Regular tasks or duties done to maintain a clean and organized home.</p>
                    <p><strong>Usage:</strong> Refers to cleaning, cooking, laundry, and other household tasks.</p>
                    <p class="example"><strong>Example:</strong> "We divide the house chores between all family members."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>living room</h3>
                    <p><strong>Definition:</strong> A room in a house for general everyday use, typically for relaxing and entertaining.</p>
                    <p><strong>Usage:</strong> The main social area of a home where people gather.</p>
                    <p class="example"><strong>Example:</strong> "We spend most of our evenings in the living room watching TV."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>phone ring</h3>
                    <p><strong>Definition:</strong> The sound a telephone makes when receiving an incoming call.</p>
                    <p><strong>Usage:</strong> Describes the auditory signal of an incoming phone call.</p>
                    <p class="example"><strong>Example:</strong> "I heard my phone ring but couldn't find it in time."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">noise</span>
                    <span class="word-option">hide</span>
                    <span class="word-option">get on</span>
                    <span class="word-option">playful</span>
                    <span class="word-option">how long does it take</span>
                    <span class="word-option">house chores</span>
                    <span class="word-option">living room</span>
                    <span class="word-option">phone ring</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="noise" onclick="selectMatch(this)">noise</div>
                    <div class="match-item" data-word="hide" onclick="selectMatch(this)">hide</div>
                    <div class="match-item" data-word="get on" onclick="selectMatch(this)">get on</div>
                    <div class="match-item" data-word="playful" onclick="selectMatch(this)">playful</div>
                    <div class="match-item" data-word="how long does it take" onclick="selectMatch(this)">how long does it take</div>
                    <div class="match-item" data-word="house chores" onclick="selectMatch(this)">house chores</div>
                    <div class="match-item" data-word="living room" onclick="selectMatch(this)">living room</div>
                    <div class="match-item" data-word="phone ring" onclick="selectMatch(this)">phone ring</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What is "noise"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Complete silence</div>
                    <div class="option" onclick="selectOption(this, true)">A loud, unpleasant, or disturbing sound</div>
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                    <div class="option" onclick="selectOption(this, false)">A colorful light</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: To "hide" means to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Show something openly</div>
                    <div class="option" onclick="selectOption(this, true)">Put or keep out of sight</div>
                    <div class="option" onclick="selectOption(this, false)">Make something louder</div>
                    <div class="option" onclick="selectOption(this, false)">Destroy something</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: "Get on" specifically means to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Get off a vehicle</div>
                    <div class="option" onclick="selectOption(this, true)">Board or enter a vehicle</div>
                    <div class="option" onclick="selectOption(this, false)">Repair a vehicle</div>
                    <div class="option" onclick="selectOption(this, false)">Buy a vehicle</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: A "playful" person or animal is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Serious and quiet</div>
                    <div class="option" onclick="selectOption(this, true)">Fond of games and amusement</div>
                    <div class="option" onclick="selectOption(this, false)">Always sleeping</div>
                    <div class="option" onclick="selectOption(this, false)">Angry and aggressive</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: "How long does it take" is a question about:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">The cost of something</div>
                    <div class="option" onclick="selectOption(this, true)">The duration or time required</div>
                    <div class="option" onclick="selectOption(this, false)">The distance to somewhere</div>
                    <div class="option" onclick="selectOption(this, false)">The quality of something</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: "House chores" are:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Entertainment activities</div>
                    <div class="option" onclick="selectOption(this, true)">Tasks to maintain a clean home</div>
                    <div class="option" onclick="selectOption(this, false)">Construction projects</div>
                    <div class="option" onclick="selectOption(this, false)">Gardening only</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7: The "living room" is typically used for:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Sleeping only</div>
                    <div class="option" onclick="selectOption(this, true)">Relaxing and entertaining guests</div>
                    <div class="option" onclick="selectOption(this, false)">Cooking meals</div>
                    <div class="option" onclick="selectOption(this, false)">Storing vehicles</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8: A "phone ring" is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A text message notification</div>
                    <div class="option" onclick="selectOption(this, true)">The sound of an incoming call</div>
                    <div class="option" onclick="selectOption(this, false)">A broken phone</div>
                    <div class="option" onclick="selectOption(this, false)">A phone accessory</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "noise", text: "A loud, unpleasant, or disturbing sound" },
            { meaning: "hide", text: "To put or keep out of sight" },
            { meaning: "get on", text: "To board or enter a vehicle" },
            { meaning: "playful", text: "Fond of games and amusement" },
            { meaning: "how long does it take", text: "A question about duration or time required" },
            { meaning: "house chores", text: "Tasks to maintain a clean and organized home" },
            { meaning: "living room", text: "A room for relaxing and entertaining" },
            { meaning: "phone ring", text: "The sound of an incoming phone call" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "The construction <input type='text' class='fill-blank' data-answer='noise' placeholder='answer'> made it difficult to concentrate.", answer: "noise" },
            { text: "The children like to <input type='text' class='fill-blank' data-answer='hide' placeholder='answer'> during games of hide and seek.", answer: "hide" },
            { text: "We need to <input type='text' class='fill-blank' data-answer='get on' placeholder='answer'> the train before it departs.", answer: "get on" },
            { text: "The puppy was very <input type='text' class='fill-blank' data-answer='playful' placeholder='answer'> and enjoyed chasing balls.", answer: "playful" },
            { text: "<input type='text' class='fill-blank' data-answer='How long does it take' placeholder='answer'> to get to the city center from here?", answer: "How long does it take" },
            { text: "We divide the <input type='text' class='fill-blank' data-answer='house chores' placeholder='answer'> between all family members.", answer: "house chores" },
            { text: "We spend most of our evenings in the <input type='text' class='fill-blank' data-answer='living room' placeholder='answer'> watching TV.", answer: "living room" },
            { text: "I heard my <input type='text' class='fill-blank' data-answer='phone ring' placeholder='answer'> but couldn't find it in time.", answer: "phone ring" },
            { text: "The constant <input type='text' class='fill-blank' data-answer='noise' placeholder='answer'> from the street kept me awake all night.", answer: "noise" },
            { text: "She tried to <input type='text' class='fill-blank' data-answer='hide' placeholder='answer'> her surprise when she saw the gift.", answer: "hide" },
            { text: "Please <input type='text' class='fill-blank' data-answer='get on' placeholder='answer'> the bus quickly so we can leave on time.", answer: "get on" },
            { text: "His <input type='text' class='fill-blank' data-answer='playful' placeholder='answer'> nature makes him popular with children.", answer: "playful" },
            { text: "<input type='text' class='fill-blank' data-answer='How long does it take' placeholder='answer'> to cook this recipe?", answer: "How long does it take" },
            { text: "Saturday morning is when we do all our <input type='text' class='fill-blank' data-answer='house chores' placeholder='answer'>.", answer: "house chores" },
            { text: "The family gathered in the <input type='text' class='fill-blank' data-answer='living room' placeholder='answer'> to open Christmas presents.", answer: "living room" },
            { text: "The loud <input type='text' class='fill-blank' data-answer='phone ring' placeholder='answer'> interrupted our conversation.", answer: "phone ring" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
