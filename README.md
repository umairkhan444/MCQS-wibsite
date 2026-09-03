<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MCQs Practice Website</title>

<style>
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    font-family:Arial,sans-serif;
}

body{
    background:#f3f6fb;
    color:#222;
}

header{
    background:linear-gradient(135deg,#2563eb,#7c3aed);
    color:white;
    text-align:center;
    padding:30px 15px;
}

header h1{
    font-size:32px;
    margin-bottom:8px;
}

header p{
    font-size:16px;
}

.container{
    max-width:900px;
    margin:25px auto;
    padding:15px;
}

/* SUBJECTS */

.subjects{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:15px;
    margin-bottom:25px;
}

.subject-btn{
    border:none;
    background:white;
    padding:20px 10px;
    border-radius:15px;
    font-size:18px;
    font-weight:bold;
    cursor:pointer;
    box-shadow:0 3px 12px rgba(0,0,0,.12);
    transition:.2s;
}

.subject-btn:hover{
    transform:translateY(-2px);
}

.subject-btn.active{
    background:#2563eb;
    color:white;
}

/* QUIZ */

.quiz-box{
    background:white;
    padding:25px;
    border-radius:16px;
    box-shadow:0 5px 20px rgba(0,0,0,.1);
}

.top{
    display:flex;
    justify-content:space-between;
    gap:10px;
    flex-wrap:wrap;
    margin-bottom:20px;
}

.badge{
    background:#eef2ff;
    color:#3730a3;
    padding:8px 12px;
    border-radius:8px;
    font-weight:bold;
}

.question{
    font-size:23px;
    font-weight:bold;
    line-height:1.5;
    margin-bottom:20px;
}

.option{
    width:100%;
    padding:15px;
    margin:8px 0;
    border:2px solid #ddd;
    border-radius:10px;
    background:white;
    text-align:left;
    font-size:17px;
    cursor:pointer;
}

.option:hover{
    border-color:#2563eb;
    background:#eff6ff;
}

.option.correct{
    border-color:#16a34a;
    background:#dcfce7;
    color:#166534;
}

.option.wrong{
    border-color:#dc2626;
    background:#fee2e2;
    color:#991b1b;
}

.feedback{
    display:none;
    margin-top:15px;
    padding:12px;
    border-radius:8px;
    font-weight:bold;
}

.feedback.correct{
    display:block;
    background:#dcfce7;
    color:#166534;
}

.feedback.wrong{
    display:block;
    background:#fee2e2;
    color:#991b1b;
}

.next-btn{
    width:100%;
    border:none;
    background:#2563eb;
    color:white;
    padding:15px;
    border-radius:10px;
    font-size:17px;
    margin-top:20px;
    cursor:pointer;
}

.next-btn:hover{
    background:#1d4ed8;
}

/* RESULT */

.result{
    display:none;
    background:white;
    text-align:center;
    padding:40px 20px;
    border-radius:16px;
    box-shadow:0 5px 20px rgba(0,0,0,.1);
}

.result h2{
    font-size:30px;
    margin-bottom:15px;
}

.score{
    font-size:50px;
    font-weight:bold;
    color:#2563eb;
    margin:20px;
}

.restart{
    border:none;
    background:#16a34a;
    color:white;
    padding:14px 25px;
    border-radius:10px;
    font-size:17px;
    cursor:pointer;
}

footer{
    text-align:center;
    color:#666;
    padding:30px;
}

/* MOBILE */

@media(max-width:600px){

    .subjects{
        grid-template-columns:1fr;
    }

    header h1{
        font-size:25px;
    }

    .question{
        font-size:19px;
    }

    .option{
        font-size:15px;
    }
}
</style>
</head>

<body>

<header>
    <h1>📚 MCQs Practice</h1>
    <p>Choose a subject and test your knowledge</p>
</header>

<div class="container">

    <!-- SUBJECT BUTTONS -->

    <div class="subjects">

        <button class="subject-btn active"
                onclick="selectSubject('English',this)">
            🇬🇧 English
        </button>

        <button class="subject-btn"
                onclick="selectSubject('Maths',this)">
            ➗ Maths
        </button>

        <button class="subject-btn"
                onclick="selectSubject('Science',this)">
            🔬 General Science
        </button>

    </div>


    <!-- QUIZ -->

    <div class="quiz-box" id="quizBox">

        <div class="top">

            <span class="badge" id="subjectName">
                English
            </span>

            <span class="badge" id="questionNumber">
                Question 1
            </span>

        </div>


        <div class="question" id="question">
            Loading...
        </div>


        <div id="options"></div>


        <div class="feedback" id="feedback"></div>


        <button class="next-btn"
                id="nextBtn"
                onclick="nextQuestion()">
            Next Question →
        </button>

    </div>


    <!-- RESULT -->

    <div class="result" id="result">

        <h2>🎉 Quiz Completed!</h2>

        <p>Your Score</p>

        <div class="score" id="finalScore">
            0 / 0
        </div>

        <p id="resultMessage"></p>

        <br>

        <button class="restart"
                onclick="restartQuiz()">
            🔄 Try Again
        </button>

    </div>

</div>


<footer>
    © 2026 MCQs Practice Website
</footer>


<script>

/* =========================================
   MCQS
========================================= */

const questions = {

English: [

{
q:"How many days are there in a week?",
options:["5","6","7","8"],
answer:2
},

{
q:"Which animal is called the king of the jungle?",
options:["Lion","Cat","Horse","Cow"],
answer:0
},

{
q:"What is the opposite of 'Hot'?",
options:["Cold","Big","Fast","Tall"],
answer:0
},

{
q:"Which word is a noun?",
options:["Run","Beautiful","School","Quickly"],
answer:2
},

{
q:"What is the plural of 'Book'?",
options:["Bookes","Books","Bookies","Book"],
answer:1
},

{
q:"Choose the correct spelling.",
options:["Frend","Freind","Friend","Freindd"],
answer:2
},

{
q:"How many vowels are there in English?",
options:["3","4","5","6"],
answer:2
},

{
q:"What is the past tense of 'Go'?",
options:["Goed","Went","Gone","Going"],
answer:1
},

{
q:"Which one is an adjective?",
options:["Beautiful","Run","School","Slowly"],
answer:0
},

{
q:"What is the opposite of 'Early'?",
options:["Fast","Late","Quick","Soon"],
answer:1
},

{
q:"Which sentence is correct?",
options:[
"He go to school.",
"He goes to school.",
"He going school.",
"He gone school."
],
answer:1
},

{
q:"What is a synonym of 'Happy'?",
options:["Sad","Angry","Glad","Weak"],
answer:2
},

{
q:"Which is a pronoun?",
options:["Ali","Book","He","School"],
answer:2
},

{
q:"What is the comparative form of 'Good'?",
options:["Gooder","Best","Better","More good"],
answer:2
},

{
q:"Which word is an adverb?",
options:["Quickly","Quick","Beauty","Run"],
answer:0
},

{
q:"What is the past participle of 'Write'?",
options:["Wrote","Writing","Written","Writes"],
answer:2
},

{
q:"How many months are there in a year?",
options:["10","11","12","13"],
answer:2
},

{
q:"Which planet is known as the Red Planet?",
options:["Earth","Mars","Venus","Jupiter"],
answer:1
},

{
q:"What is the opposite of 'Big'?",
options:["Large","Small","Tall","Long"],
answer:1
},

{
q:"Which word is a verb?",
options:["Run","Beautiful","Blue","School"],
answer:0
}

],


Maths: [

{
q:"5 + 7 = ?",
options:["10","11","12","13"],
answer:2
},

{
q:"10 × 2 = ?",
options:["12","20","22","30"],
answer:1
},

{
q:"20 - 8 = ?",
options:["10","11","12","13"],
answer:2
},

{
q:"25 + 35 = ?",
options:["50","60","70","55"],
answer:1
},

{
q:"8 × 7 = ?",
options:["54","56","58","64"],
answer:1
},

{
q:"100 ÷ 10 = ?",
options:["5","10","20","100"],
answer:1
},

{
q:"12 × 12 = ?",
options:["124","144","154","164"],
answer:1
},

{
q:"What is 15% of 100?",
options:["10","15","20","25"],
answer:1
},

{
q:"2³ = ?",
options:["4","6","8","10"],
answer:2
},

{
q:"If x + 5 = 12, what is x?",
options:["5","6","7","8"],
answer:2
},

{
q:"What is the square root of 81?",
options:["7","8","9","10"],
answer:2
},

{
q:"10 + 20 = ?",
options:["20","25","30","35"],
answer:2
},

{
q:"50 - 25 = ?",
options:["15","20","25","30"],
answer:2
},

{
q:"6 × 6 = ?",
options:["30","36","42","48"],
answer:1
},

{
q:"72 ÷ 8 = ?",
options:["7","8","9","10"],
answer:2
},

{
q:"What is half of 20?",
options:["5","10","15","20"],
answer:1
},

{
q:"9 + 11 = ?",
options:["18","19","20","21"],
answer:2
},

{
q:"15 × 2 = ?",
options:["20","25","30","35"],
answer:2
},

{
q:"100 - 45 = ?",
options:["45","50","55","65"],
answer:2
},

{
q:"4 × 5 = ?",
options:["15","20","25","30"],
answer:1
}

],


Science: [

{
q:"Which planet do we live on?",
options:["Mars","Earth","Jupiter","Venus"],
answer:1
},

{
q:"How many legs does a spider have?",
options:["4","6","8","10"],
answer:2
},

{
q:"Which organ helps us breathe?",
options:["Heart","Lungs","Brain","Stomach"],
answer:1
},

{
q:"The Sun is a...?",
options:["Planet","Star","Moon","Rock"],
answer:1
},

{
q:"Water freezes at?",
options:["0°C","10°C","50°C","100°C"],
answer:0
},

{
q:"Plants make food using?",
options:[
"Photosynthesis",
"Digestion",
"Respiration",
"Evaporation"
],
answer:0
},

{
q:"Which gas do humans need for breathing?",
options:[
"Carbon dioxide",
"Oxygen",
"Nitrogen",
"Hydrogen"
],
answer:1
},

{
q:"What is the center of an atom called?",
options:["Cell","Nucleus","Organ","Molecule"],
answer:1
},

{
q:"Which force pulls objects toward Earth?",
options:[
"Magnetic force",
"Gravity",
"Friction",
"Electricity"
],
answer:1
},

{
q:"What is H2O?",
options:["Oxygen","Hydrogen","Water","Salt"],
answer:2
},

{
q:"Which organ pumps blood around the body?",
options:["Brain","Heart","Lungs","Stomach"],
answer:1
},

{
q:"What do plants need to make food?",
options:["Sunlight","Plastic","Iron","Glass"],
answer:0
},

{
q:"Which animal lays eggs?",
options:["Dog","Cat","Hen","Cow"],
answer:2
},

{
q:"What is the largest planet in our solar system?",
options:["Earth","Mars","Jupiter","Venus"],
answer:2
},

{
q:"Which part of a plant absorbs water?",
options:["Flower","Root","Fruit","Leaf"],
answer:1
},

{
q:"How many planets are in our solar system?",
options:["6","7","8","9"],
answer:2
},

{
q:"Which gas do plants take in?",
options:["Oxygen","Carbon dioxide","Hydrogen","Helium"],
answer:1
},

{
q:"What gives Earth light and heat?",
options:["Moon","Sun","Mars","Stars"],
answer:1
},

{
q:"Which sense organ helps us see?",
options:["Ear","Eye","Nose","Skin"],
answer:1
},

{
q:"What is the natural satellite of Earth?",
options:["Sun","Mars","Moon","Venus"],
answer:2
}

]

};


/* =========================================
   VARIABLES
========================================= */

let currentSubject = "English";
let currentQuestion = 0;
let score = 0;
let answered = false;


/* =========================================
   LOAD QUESTION
========================================= */

function loadQuestion(){

    const list = questions[currentSubject];

    const item = list[currentQuestion];

    document.getElementById("subjectName").innerText =
        currentSubject;

    document.getElementById("questionNumber").innerText =
        "Question " +
        (currentQuestion + 1) +
        " / " +
        list.length;

    document.getElementById("question").innerText =
        item.q;

    const optionsDiv =
        document.getElementById("options");

    optionsDiv.innerHTML = "";

    document.getElementById("feedback").className =
        "feedback";

    document.getElementById("feedback").innerText =
        "";

    answered = false;


    item.options.forEach(function(option,index){

        const button =
            document.createElement("button");

        button.className = "option";

        button.innerText =
            String.fromCharCode(65 + index) +
            ". " + option;

        button.onclick = function(){

            checkAnswer(index,button);

        };

        optionsDiv.appendChild(button);

    });

}


/* =========================================
   CHECK ANSWER
========================================= */

function checkAnswer(selected,button){

    if(answered){
        return;
    }

    answered = true;

    const list = questions[currentSubject];

    const correct =
        list[currentQuestion].answer;

    const allButtons =
        document.querySelectorAll(".option");


    if(selected === correct){

        score++;

        button.classList.add("correct");

        document.getElementById("feedback").className =
            "feedback correct";

        document.getElementById("feedback").innerText =
            "✅ Correct Answer!";

    }else{

        button.classList.add("wrong");

        document.getElementById("feedback").className =
            "feedback wrong";

        document.getElementById("feedback").innerText =
            "❌ Wrong Answer!";

        allButtons[correct].classList.add("correct");

    }

}


/* =========================================
   NEXT QUESTION
========================================= */

function nextQuestion(){

    if(!answered){

        alert("Please select an answer first.");

        return;
    }

    const list = questions[currentSubject];

    currentQuestion++;


    if(currentQuestion >= list.length){

        showResult();

    }else{

        loadQuestion();

    }

}


/* =========================================
   RESULT
========================================= */

function showResult(){

    document.getElementById("quizBox").style.display =
        "none";

    document.getElementById("result").style.display =
        "block";


    const total =
        questions[currentSubject].length;

    document.getElementById("finalScore").innerText =
        score + " / " + total;


    const percentage =
        Math.round((score / total) * 100);


    let message;


    if(percentage >= 80){

        message =
            "🌟 Excellent! Very Good Work!";

    }else if(percentage >= 50){

        message =
            "👍 Good! Keep Practicing!";

    }else{

        message =
            "📚 Keep Learning and Try Again!";

    }


    document.getElementById("resultMessage").innerText =
        message +
        " You scored " +
        percentage +
        "%.";

}


/* =========================================
   SELECT SUBJECT
========================================= */

function selectSubject(subject,button){

    currentSubject = subject;

    currentQuestion = 0;

    score = 0;

    answered = false;


    document.querySelectorAll(".subject-btn")
        .forEach(function(btn){

            btn.classList.remove("active");

        });


    button.classList.add("active");


    document.getElementById("quizBox").style.display =
        "block";

    document.getElementById("result").style.display =
        "none";


    loadQuestion();

}


/* =========================================
   RESTART
========================================= */

function restartQuiz(){

    currentQuestion = 0;

    score = 0;

    answered = false;


    document.getElementById("quizBox").style.display =
        "block";

    document.getElementById("result").style.display =
        "none";


    loadQuestion();

}


/* =========================================
   START
========================================= */

loadQuestion();

</script>

</body>
</html>
