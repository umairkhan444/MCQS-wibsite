<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MCQS Website</title>

<style>
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    font-family:Arial, sans-serif;
}

body{
    background:#f2f6ff;
    color:#222;
}

header{
    background:linear-gradient(135deg,#2563eb,#7c3aed);
    color:white;
    padding:25px 15px;
    text-align:center;
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

/* Tabs */
.tabs{
    display:flex;
    gap:10px;
    justify-content:center;
    flex-wrap:wrap;
    margin-bottom:20px;
}

.tab{
    border:none;
    padding:12px 25px;
    border-radius:10px;
    background:white;
    color:#333;
    font-size:16px;
    cursor:pointer;
    box-shadow:0 2px 8px rgba(0,0,0,.1);
}

.tab:hover,
.tab.active{
    background:#2563eb;
    color:white;
}

/* Class buttons */
.classes{
    display:flex;
    justify-content:center;
    gap:10px;
    flex-wrap:wrap;
    margin-bottom:25px;
}

.classBtn{
    border:none;
    padding:10px 18px;
    border-radius:8px;
    background:#e5e7eb;
    cursor:pointer;
    font-size:15px;
}

.classBtn.active{
    background:#16a34a;
    color:white;
}

/* Quiz */
.quiz-box{
    background:white;
    border-radius:15px;
    padding:25px;
    box-shadow:0 5px 20px rgba(0,0,0,.1);
}

.quiz-header{
    display:flex;
    justify-content:space-between;
    gap:10px;
    margin-bottom:20px;
    flex-wrap:wrap;
}

.badge{
    background:#eef2ff;
    color:#4338ca;
    padding:8px 12px;
    border-radius:8px;
    font-weight:bold;
}

.question{
    font-size:22px;
    font-weight:bold;
    margin-bottom:20px;
    line-height:1.5;
}

.option{
    width:100%;
    border:2px solid #ddd;
    background:white;
    padding:14px;
    margin:10px 0;
    border-radius:10px;
    text-align:left;
    font-size:17px;
    cursor:pointer;
    transition:.2s;
}

.option:hover{
    border-color:#2563eb;
    background:#eff6ff;
}

.option.correct{
    background:#dcfce7;
    border-color:#16a34a;
    color:#166534;
}

.option.wrong{
    background:#fee2e2;
    border-color:#dc2626;
    color:#991b1b;
}

.feedback{
    margin-top:15px;
    padding:12px;
    border-radius:8px;
    display:none;
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
    margin-top:20px;
    width:100%;
    padding:14px;
    border:none;
    background:#2563eb;
    color:white;
    font-size:17px;
    border-radius:10px;
    cursor:pointer;
}

.next-btn:hover{
    background:#1d4ed8;
}

/* Result */
.result{
    display:none;
    text-align:center;
    background:white;
    padding:35px 20px;
    border-radius:15px;
    box-shadow:0 5px 20px rgba(0,0,0,.1);
}

.result h2{
    font-size:30px;
    margin-bottom:15px;
}

.score{
    font-size:45px;
    font-weight:bold;
    color:#2563eb;
    margin:15px;
}

.restart{
    border:none;
    background:#16a34a;
    color:white;
    padding:13px 25px;
    border-radius:10px;
    font-size:16px;
    cursor:pointer;
}

footer{
    text-align:center;
    padding:25px;
    color:#666;
}

@media(max-width:600px){
    header h1{
        font-size:25px;
    }

    .question{
        font-size:19px;
    }

    .option{
        font-size:15px;
    }

    .tab{
        padding:10px 16px;
    }
}
</style>
</head>

<body>

<header>
    <h1>📚 MCQS Learning Website</h1>
    <p>Class 3rd to 7th - Learn & Test Your Knowledge</p>
</header>

<div class="container">

    <!-- Subject Tabs -->
    <div class="tabs">
        <button class="tab active" onclick="selectSubject('English',this)">
            🇬🇧 English
        </button>

        <button class="tab" onclick="selectSubject('Urdu',this)">
            🇵🇰 Urdu
        </button>

        <button class="tab" onclick="selectSubject('Maths',this)">
            ➗ Maths
        </button>

        <button class="tab" onclick="selectSubject('Science',this)">
            🔬 Science
        </button>
    </div>

    <!-- Classes -->
    <div class="classes">
        <button class="classBtn active" onclick="selectClass(3,this)">Class 3</button>
        <button class="classBtn" onclick="selectClass(4,this)">Class 4</button>
        <button class="classBtn" onclick="selectClass(5,this)">Class 5</button>
        <button class="classBtn" onclick="selectClass(6,this)">Class 6</button>
        <button class="classBtn" onclick="selectClass(7,this)">Class 7</button>
    </div>

    <!-- Quiz -->
    <div class="quiz-box" id="quizBox">

        <div class="quiz-header">
            <span class="badge" id="subjectName">English</span>
            <span class="badge" id="className">Class 3</span>
            <span class="badge" id="questionNumber">Question 1</span>
        </div>

        <div class="question" id="question">
            Loading question...
        </div>

        <div id="options"></div>

        <div class="feedback" id="feedback"></div>

        <button class="next-btn" onclick="nextQuestion()" id="nextBtn">
            Next Question →
        </button>

    </div>

    <!-- Result -->
    <div class="result" id="result">

        <h2>🎉 Quiz Completed!</h2>

        <p>Your Score</p>

        <div class="score" id="finalScore">
            0 / 0
        </div>

        <p id="resultMessage"></p>

        <br>

        <button class="restart" onclick="restartQuiz()">
            🔄 Try Again
        </button>

    </div>

</div>

<footer>
    © 2026 MCQS Learning Website
</footer>


<script>

/* =========================
   QUESTIONS
========================= */

const questions = {

English: {

3:[
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
}
],

4:[
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
}
],

5:[
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
}
],

6:[
{
q:"Which is a pronoun?",
options:["Ali","Book","He","School"],
answer:2
},
{
q:"What is the comparative form of 'Good'?",
options:["Gooder","Best","Better","More good"],
answer:2
}
],

7:[
{
q:"Which word is an adverb?",
options:["Quickly","Quick","Beauty","Run"],
answer:0
},
{
q:"What is the past participle of 'Write'?",
options:["Wrote","Writing","Written","Writes"],
answer:2
}
]

},


Urdu:{

3:[
{
q:"پاکستان کا قومی پھول کون سا ہے؟",
options:["گلاب","چنبیلی","سورج مکھی","نرگس"],
answer:1
},
{
q:"الفاظ 'کتاب' کی جمع کیا ہے؟",
options:["کتابیں","کتابان","کتابی","کتابوں"],
answer:0
}
],

4:[
{
q:"اسم کسے کہتے ہیں؟",
options:[
"کام کو",
"نام کو",
"صفت کو",
"فعل کو"
],
answer:1
},
{
q:"لفظ 'خوبصورت' کیا ہے؟",
options:["اسم","فعل","صفت","ضمیر"],
answer:2
}
],

5:[
{
q:"فعل کیا ظاہر کرتا ہے؟",
options:["نام","کام","جگہ","چیز"],
answer:1
},
{
q:"'لڑکا' کی جمع کیا ہے؟",
options:["لڑکی","لڑکے","لڑکیاں","لڑکوں"],
answer:1
}
],

6:[
{
q:"اردو زبان کس رسم الخط میں لکھی جاتی ہے؟",
options:["رومن","عربی فارسی","دیوناگری","چینی"],
answer:1
}
],

7:[
{
q:"مترادف الفاظ سے کیا مراد ہے؟",
options:[
"الٹ معنی والے الفاظ",
"ایک جیسے معنی والے الفاظ",
"غلط الفاظ",
"مشکل الفاظ"
],
answer:1
}
]

},


Maths:{

3:[
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
}
],

4:[
{
q:"25 + 35 = ?",
options:["50","60","70","55"],
answer:1
},
{
q:"8 × 7 = ?",
options:["54","56","58","64"],
answer:1
}
],

5:[
{
q:"100 ÷ 10 = ?",
options:["5","10","20","100"],
answer:1
},
{
q:"12 × 12 = ?",
options:["124","144","154","164"],
answer:1
}
],

6:[
{
q:"What is 15% of 100?",
options:["10","15","20","25"],
answer:1
},
{
q:"2³ = ?",
options:["4","6","8","10"],
answer:2
}
],

7:[
{
q:"If x + 5 = 12, what is x?",
options:["5","6","7","8"],
answer:2
},
{
q:"What is the square root of 81?",
options:["7","8","9","10"],
answer:2
}
]

},


Science:{

3:[
{
q:"Which planet do we live on?",
options:["Mars","Earth","Jupiter","Venus"],
answer:1
},
{
q:"How many legs does a spider have?",
options:["4","6","8","10"],
answer:2
}
],

4:[
{
q:"Which organ helps us breathe?",
options:["Heart","Lungs","Brain","Stomach"],
answer:1
},
{
q:"The Sun is a...?",
options:["Planet","Star","Moon","Rock"],
answer:1
}
],

5:[
{
q:"Water freezes at?",
options:["0°C","10°C","50°C","100°C"],
answer:0
},
{
q:"Plants make food using?",
options:["Photosynthesis","Digestion","Respiration","Evaporation"],
answer:0
}
],

6:[
{
q:"Which gas do humans need for breathing?",
options:["Carbon dioxide","Oxygen","Nitrogen","Hydrogen"],
answer:1
},
{
q:"What is the center of an atom called?",
options:["Cell","Nucleus","Organ","Molecule"],
answer:1
}
],

7:[
{
q:"Which force pulls objects toward Earth?",
options:["Magnetic force","Gravity","Friction","Electricity"],
answer:1
},
{
q:"What is H2O?",
options:["Oxygen","Hydrogen","Water","Salt"],
answer:2
}
]

}

};


/* =========================
   VARIABLES
========================= */

let currentSubject = "English";
let currentClass = 3;
let currentQuestion = 0;
let score = 0;
let answered = false;


/* =========================
   LOAD QUESTION
========================= */

function loadQuestion(){

    const list =
        questions[currentSubject][currentClass];

    if(!list || list.length === 0){

        document.getElementById("question").innerText =
        "Questions coming soon...";

        document.getElementById("options").innerHTML = "";

        return;
    }

    const item = list[currentQuestion];

    document.getElementById("subjectName").innerText =
        currentSubject;

    document.getElementById("className").innerText =
        "Class " + currentClass;

    document.getElementById("questionNumber").innerText =
        "Question " + (currentQuestion + 1) +
        " / " + list.length;

    document.getElementById("question").innerText =
        item.q;

    const optionsDiv =
        document.getElementById("options");

    optionsDiv.innerHTML = "";

    document.getElementById("feedback").className =
        "feedback";

    document.getElementById("feedback").innerText = "";

    answered = false;

    item.options.forEach((option,index)=>{

        const button =
            document.createElement("button");

        button.className = "option";

        button.innerText =
            String.fromCharCode(65+index) +
            ". " + option;

        button.onclick = function(){

            checkAnswer(index,button);

        };

        optionsDiv.appendChild(button);

    });

}


/* =========================
   CHECK ANSWER
========================= */

function checkAnswer(selected,button){

    if(answered) return;

    answered = true;

    const list =
        questions[currentSubject][currentClass];

    const correct =
        list[currentQuestion].answer;

    const allButtons =
        document.querySelectorAll(".option");

    allButtons.forEach((btn,index)=>{

        if(index === correct){

            btn.classList.add("correct");

        }

    });


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
            "❌ Wrong Answer! Correct answer is: " +
            list[currentQuestion].options[correct];

    }

}


/* =========================
   NEXT QUESTION
========================= */

function nextQuestion(){

    const list =
        questions[currentSubject][currentClass];

    if(!answered){

        alert("Please select an answer first.");

        return;
    }

    currentQuestion++;

    if(currentQuestion >= list.length){

        showResult();

    }else{

        loadQuestion();

    }

}


/* =========================
   RESULT
========================= */

function showResult(){

    document.getElementById("quizBox").style.display =
        "none";

    document.getElementById("result").style.display =
        "block";

    const total =
        questions[currentSubject][currentClass].length;

    document.getElementById("finalScore").innerText =
        score + " / " + total;

    let percentage =
        Math.round((score / total) * 100);

    let message = "";

    if(percentage >= 80){

        message = "🌟 Excellent! Very Good Work!";

    }else if(percentage >= 50){

        message = "👍 Good! Keep Practicing!";

    }else{

        message = "📚 Keep Learning and Try Again!";

    }

    document.getElementById("resultMessage").innerText =
        message + " You scored " + percentage + "%.";

}


/* =========================
   RESTART
========================= */

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


/* =========================
   SUBJECT
========================= */

function selectSubject(subject,button){

    currentSubject = subject;

    currentQuestion = 0;

    score = 0;

    document.querySelectorAll(".tab")
        .forEach(btn=>btn.classList.remove("active"));

    button.classList.add("active");

    document.getElementById("quizBox").style.display =
        "block";

    document.getElementById("result").style.display =
        "none";

    loadQuestion();

}


/* =========================
   CLASS
========================= */

function selectClass(classNumber,button){

    currentClass = classNumber;

    currentQuestion = 0;

    score = 0;

    document.querySelectorAll(".classBtn")
        .forEach(btn=>btn.classList.remove("active"));

    button.classList.add("active");

    document.getElementById("quizBox").style.display =
        "block";

    document.getElementById("result").style.display =
        "none";

    loadQuestion();

}


/* Start */

loadQuestion();

</script>

</body>
</html>
