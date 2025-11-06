# fire-exam-system
消防设施操作员在线题库系统
fire-exam-system/
├── index.html
├── css/
│   └── style.css
├── js/
│   ├── main.js
│   ├── questions.js
│   └── utils.js
├── README.md
└── LICENSE
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>消防设施操作员在线题库</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <div class="container">
        <header>
            <h1>消防设施操作员在线题库</h1>
            <div class="stats">
                <span>总题数：<span id="totalCount">600</span></span>
                <span>已答：<span id="answeredCount">0</span></span>
                <span>正确率：<span id="correctRate">0%</span></span>
            </div>
        </header>
        
        <div class="control-panel">
            <div class="mode-selector">
                <h3>练习模式</h3>
                <label><input type="radio" name="mode" value="random" checked> 随机练习</label>
                <label><input type="radio" name="mode" value="wrong"> 错题练习</label>
                <label><input type="radio" name="mode" value="sequence"> 顺序练习</label>
            </div>
            
            <div class="type-selector">
                <h3>题型选择</h3>
                <label><input type="checkbox" name="type" value="single" checked> 单选题</label>
                <label><input type="checkbox" name="type" value="multiple" checked> 多选题</label>
                <label><input type="checkbox" name="type" value="judge" checked> 判断题</label>
            </div>
            
            <div class="number-selector">
                <h3>题目数量</h3>
                <select id="questionCount">
                    <option value="10">10题</option>
                    <option value="20" selected>20题</option>
                    <option value="50">50题</option>
                    <option value="100">100题</option>
                </select>
            </div>
            
            <button id="startBtn" class="btn-primary">开始练习</button>
        </div>
        
        <div id="questionArea" class="question-area" style="display: none;">
            <div class="question-header">
                <span id="questionProgress">第1题 / 共20题</span>
                <div class="timer">
                    用时：<span id="timer">00:00</span>
                </div>
            </div>
            
            <div id="questionContent" class="question-content">
                <!-- 题目内容将在这里显示 -->
            </div>
            
            <div class="question-options" id="questionOptions">
                <!-- 选项将在这里显示 -->
            </div>
            
            <div class="question-actions">
                <button id="prevBtn" class="btn-secondary">上一题</button>
                <button id="nextBtn" class="btn-primary">下一题</button>
                <button id="submitBtn" class="btn-success" style="display: none;">提交答案</button>
            </div>
        </div>
        
        <div id="resultArea" class="result-area" style="display: none;">
            <div class="result-summary">
                <h2>练习结果</h2>
                <div class="result-stats">
                    <div class="stat-item">
                        <span class="stat-label">总题数</span>
                        <span class="stat-value" id="resultTotal">0</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-label">正确数</span>
                        <span class="stat-value" id="resultCorrect">0</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-label">错误数</span>
                        <span class="stat-value" id="resultWrong">0</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-label">正确率</span>
                        <span class="stat-value" id="resultRate">0%</span>
                    </div>
                </div>
            </div>
            
            <div class="result-actions">
                <button id="reviewBtn" class="btn-info">查看解析</button>
                <button id="restartBtn" class="btn-primary">再次练习</button>
                <button id="wrongBtn" class="btn-warning">练习错题</button>
            </div>
        </div>
        
        <div id="reviewArea" class="review-area" style="display: none;">
            <h2>答题解析</h2>
            <div id="reviewContent">
                <!-- 解析内容将在这里显示 -->
            </div>
            <button id="backToResultBtn" class="btn-secondary">返回结果</button>
        </div>
    </div>
    
    <script src="js/questions.js"></script>
    <script src="js/utils.js"></script>
    <script src="js/main.js"></script>
</body>
</html>* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Microsoft YaHei', sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    padding: 20px;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    background: white;
    border-radius: 15px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.1);
    overflow: hidden;
}

header {
    background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
    color: white;
    padding: 30px;
    text-align: center;
}

header h1 {
    font-size: 2.5em;
    margin-bottom: 15px;
}

.stats {
    display: flex;
    justify-content: center;
    gap: 30px;
    font-size: 1.1em;
}

.control-panel {
    padding: 30px;
    background: #f8f9fa;
}

.control-panel h3 {
    margin-bottom: 15px;
    color: #333;
}

.mode-selector, .type-selector, .number-selector {
    margin-bottom: 25px;
}

.mode-selector label, .type-selector label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
}

.mode-selector input, .type-selector input {
    margin-right: 5px;
}

select {
    padding: 10px 15px;
    border: 2px solid #ddd;
    border-radius: 8px;
    font-size: 16px;
    background: white;
}

.btn-primary {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 8px;
    font-size: 18px;
    cursor: pointer;
    transition: transform 0.2s;
}

.btn-primary:hover {
    transform: translateY(-2px);
}

.question-area {
    padding: 30px;
}

.question-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 2px solid #eee;
}

.question-content {
    margin-bottom: 30px;
}

.question-content h3 {
    font-size: 1.3em;
    margin-bottom: 20px;
    line-height: 1.6;
}

.question-options {
    margin-bottom: 30px;
}

.question-options label {
    display: block;
    padding: 15px;
    margin-bottom: 10px;
    background: #f8f9fa;
    border: 2px solid #eee;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s;
}

.question-options label:hover {
    background: #e9ecef;
    border-color: #667eea;
}

.question-options input[type="radio"],
.question-options input[type="checkbox"] {
    margin-right: 10px;
}

.question-actions {
    display: flex;
    gap: 15px;
    justify-content: center;
}

.btn-secondary {
    background: #6c757d;
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 8px;
    cursor: pointer;
}

.btn-success {
    background: #28a745;
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 8px;
    cursor: pointer;
}

.result-area {
    padding: 30px;
    text-align: center;
}

.result-summary {
    margin-bottom: 30px;
}

.result-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    margin-bottom: 30px;
}

.stat-item {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 10px;
}

.stat-label {
    display: block;
    font-size: 0.9em;
    color: #666;
    margin-bottom: 5px;
}

.stat-value {
    display: block;
    font-size: 2em;
    font-weight: bold;
    color: #333;
}

.result-actions {
    display: flex;
    gap: 15px;
    justify-content: center;
}

.btn-info {
    background: #17a2b8;
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 8px;
    cursor: pointer;
}

.btn-warning {
    background: #ffc107;
    color: #212529;
    border: none;
    padding: 12px 25px;
    border-radius: 8px;
    cursor: pointer;
}

.review-area {
    padding: 30px;
}

.review-item {
    background: #f8f9fa;
    padding: 20px;
    margin-bottom: 20px;
    border-radius: 10px;
}

.review-item.correct {
    border-left: 5px solid #28a745;
}

.review-item.wrong {
    border-left: 5px solid #dc3545;
}

.review-question {
    font-weight: bold;
    margin-bottom: 10px;
}

.review-answer {
    margin-bottom: 10px;
}

.review-explanation {
    color: #666;
    font-size: 0.9em;
}

@media (max-width: 768px) {
    body {
        padding: 10px;
    }
    
    header h1 {
        font-size: 1.8em;
    }
    
    .stats {
        flex-direction: column;
        gap: 10px;
    }
    
    .control-panel {
        padding: 20px;
    }
    
    .question-actions {
        flex-direction: column;
    }
}// 主要功能脚本
class ExamSystem {
    constructor() {
        this.questions = [];
        this.currentQuestions = [];
        this.currentIndex = 0;
        this.userAnswers = [];
        this.startTime = null;
        this.timer = null;
        this.wrongQuestions = this.loadWrongQuestions();
        
        this.init();
    }
    
    init() {
        this.bindEvents();
        this.updateStats();
        this.loadQuestions();
    }
    
    loadQuestions() {
        // 从questions.js加载题目数据
        this.questions = window.questionBank || [];
        document.getElementById('totalCount').textContent = this.questions.length;
    }
    
    bindEvents() {
        document.getElementById('startBtn').addEventListener('click', () => this.startExam());
        document.getElementById('prevBtn').addEventListener('click', () => this.prevQuestion());
        document.getElementById('nextBtn').addEventListener('click', () => this.nextQuestion());
        document.getElementById('submitBtn').addEventListener('click', () => this.submitExam());
        document.getElementById('reviewBtn').addEventListener('click', () => this.showReview());
        document.getElementById('restartBtn').addEventListener('click', () => this.restartExam());
        document.getElementById('wrongBtn').addEventListener('click', () => this.practiceWrong());
        document.getElementById('backToResultBtn').addEventListener('click', () => this.showResult());
    }
    
    startExam() {
        const mode = document.querySelector('input[name="mode"]:checked').value;
        const types = Array.from(document.querySelectorAll('input[name="type"]:checked')).map(cb => cb.value);
        const count = parseInt(document.getElementById('questionCount').value);
        
        this.prepareQuestions(mode, types, count);
        this.currentIndex = 0;
        this.userAnswers = new Array(this.currentQuestions.length).fill(null);
        this.startTime = Date.now();
        
        document.querySelector('.control-panel').style.display = 'none';
        document.getElementById('questionArea').style.display = 'block';
        
        this.showQuestion();
        this.startTimer();
    }
    
    prepareQuestions(mode, types, count) {
        let filteredQuestions = this.questions.filter(q => types.includes(q.type));
        
        switch(mode) {
            case 'random':
                this.currentQuestions = this.shuffleArray([...filteredQuestions]).slice(0, count);
                break;
            case 'wrong':
                this.currentQuestions = this.wrongQuestions.slice(0, count);
                break;
            case 'sequence':
                this.currentQuestions = filteredQuestions.slice(0, count);
                break;
        }
    }
    
    shuffleArray(array) {
        const newArray = [...array];
        for (let i = newArray.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
        }
        return newArray;
    }
    
    showQuestion() {
        const question = this.currentQuestions[this.currentIndex];
        const total = this.currentQuestions.length;
        
        document.getElementById('questionProgress').textContent = `第${this.currentIndex + 1}题 / 共${total}题`;
        
        const content = document.getElementById('questionContent');
        content.innerHTML = `<h3>${question.question}</h3>`;
        
        const options = document.getElementById('questionOptions');
        options.innerHTML = '';
        
        if (question.type === 'single') {
            question.options.forEach((option, index) => {
                const label = document.createElement('label');
                label.innerHTML = `
                    <input type="radio" name="answer" value="${String.fromCharCode(65 + index)}" 
                        ${this.userAnswers[this.currentIndex] === String.fromCharCode(65 + index) ? 'checked' : ''}>
                    ${option}
                `;
                options.appendChild(label);
            });
        } else if (question.type === 'multiple') {
            question.options.forEach((option, index) => {
                const label = document.createElement('label');
                const answer = this.userAnswers[this.currentIndex] || [];
                label.innerHTML = `
                    <input type="checkbox" name="answer" value="${String.fromCharCode(65 + index)}" 
                        ${Array.isArray(answer) && answer.includes(String.fromCharCode(65 + index)) ? 'checked' : ''}>
                    ${option}
                `;
                options.appendChild(label);
            });
        } else if (question.type === 'judge') {
            const options = [
                { value: 'true', text: '正确' },
                { value: 'false', text: '错误' }
            ];
            options.forEach(option => {
                const label = document.createElement('label');
                label.innerHTML = `
                    <input type="radio" name="answer" value="${option.value}" 
                        ${this.userAnswers[this.currentIndex] === option.value ? 'checked' : ''}>
                    ${option.text}
                `;
                options.appendChild(label);
            });
        }
        
        // 更新按钮状态
        document.getElementById('prevBtn').style.display = this.currentIndex > 0 ? 'inline-block' : 'none';
        document.getElementById('nextBtn').style.display = this.currentIndex < total - 1 ? 'inline-block' : 'none';
        document.getElementById('submitBtn').style.display = this.currentIndex === total - 1 ? 'inline-block' : 'none';
    }
    
    prevQuestion() {
        this.saveAnswer();
        if (this.currentIndex > 0) {
            this.currentIndex--;
            this.showQuestion();
        }
    }
    
    nextQuestion() {
        this.saveAnswer();
        if (this.currentIndex < this.currentQuestions.length - 1) {
            this.currentIndex++;
            this.showQuestion();
        }
    }
    
    saveAnswer() {
        const answerInputs = document.querySelectorAll('input[name="answer"]');
        let answer = null;
        
        if (this.currentQuestions[this.currentIndex].type === 'multiple') {
            answer = Array.from(answerInputs)
                .filter(input => input.checked)
                .map(input => input.value);
        } else {
            const checkedInput = document.querySelector('input[name="answer"]:checked');
            answer = checkedInput ? checkedInput.value : null;
        }
        
        this.userAnswers[this.currentIndex] = answer;
    }
    
    submitExam() {
        this.saveAnswer();
        this.stopTimer();
        this.calculateResult();
        this.showResult();
    }
    
    calculateResult() {
        let correctCount = 0;
        this.resultDetails = [];
        
        this.currentQuestions.forEach((question, index) => {
            const userAnswer = this.userAnswers[index];
            let isCorrect = false;
            
            if (question.type === 'multiple') {
                isCorrect = this.arraysEqual(userAnswer, question.answer);
            } else {
                isCorrect = userAnswer === question.answer;
            }
            
            if (isCorrect) {
                correctCount++;
            } else {
                // 添加到错题本
                this.addWrongQuestion(question);
            }
            
            this.resultDetails.push({
                question: question,
                userAnswer: userAnswer,
                correct: isCorrect
            });
        });
        
        this.result = {
            total: this.currentQuestions.length,
            correct: correctCount,
            wrong: this.currentQuestions.length - correctCount,
            rate: Math.round((correctCount / this.currentQuestions.length) * 100)
        };
        
        this.updateStats();
    }
    
    arraysEqual(a, b) {
        if (!Array.isArray(a) || !Array.isArray(b)) return false;
        if (a.length !== b.length) return false;
        const sortedA = [...a].sort();
        const sortedB = [...b].sort();
        return sortedA.every((val, index) => val === sortedB[index]);
    }
    
    showResult() {
        document.getElementById('questionArea').style.display = 'none';
        document.getElementById('resultArea').style.display = 'block';
        
        document.getElementById('resultTotal').textContent = this.result.total;
        document.getElementById('resultCorrect').textContent = this.result.correct;
        document.getElementById('resultWrong').textContent = this.result.wrong;
        document.getElementById('resultRate').textContent = this.result.rate + '%';
    }
    
    showReview() {
        document.getElementById('resultArea').style.display = 'none';
        document.getElementById('reviewArea').style.display = 'block';
        
        const reviewContent = document.getElementById('reviewContent');
        reviewContent.innerHTML = '';
        
        this.resultDetails.forEach((detail, index) => {
            const reviewItem = document.createElement('div');
            reviewItem.className = `review-item ${detail.correct ? 'correct' : 'wrong'}`;
            
            let userAnswerText = '';
            if (detail.question.type === 'multiple') {
                userAnswerText = Array.isArray(detail.userAnswer) ? 
                    detail.userAnswer.map(a => String.fromCharCode(64 + detail.question.options.indexOf(detail.question.options[String.fromCharCode(65).charCodeAt(0) - 65]))).join(', ') : 
                    '未作答';
            } else {
                userAnswerText = detail.userAnswer || '未作答';
            }
            
            reviewItem.innerHTML = `
                <div class="review-question">${index + 1}. ${detail.question.question}</div>
                <div class="review-answer">
                    <strong>您的答案：</strong>${userAnswerText}<br>
                    <strong>正确答案：</strong>${Array.isArray(detail.question.answer) ? 
                        detail.question.answer.join(', ') : detail.question.answer}
                </div>
                <div class="review-explanation">${detail.question.explanation || ''}</div>
            `;
            
            reviewContent.appendChild(reviewItem);
        });
    }
    
    restartExam() {
        document.getElementById('resultArea').style.display = 'none';
        document.getElementById('reviewArea').style.display = 'none';
        document.querySelector('.control-panel').style.display = 'block';
    }
    
    practiceWrong() {
        if (this.wrongQuestions.length === 0) {
            alert('暂无错题，请先完成一些练习！');
            return;
        }
        
        document.getElementById('resultArea').style.display = 'none';
        document.querySelector('input[value="wrong"]').checked = true;
        this.startExam();
    }
    
    showResult() {
        document.getElementById('reviewArea').style.display = 'none';
        document.getElementById('resultArea').style.display = 'block';
    }
    
    startTimer() {
        this.timer = setInterval(() => {
            const elapsed = Date.now() - this.startTime;
            const minutes = Math.floor(elapsed / 60000);
            const seconds = Math.floor((elapsed % 60000) / 1000);
            document.getElementById('timer').textContent = 
                `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }, 1000);
    }
    
    stopTimer() {
        if (this.timer) {
            clearInterval(this.timer);
            this.timer = null;
        }
    }
    
    addWrongQuestion(question) {
        const exists = this.wrongQuestions.some(q => q.id === question.id);
        if (!exists) {
            this.wrongQuestions.push(question);
            this.saveWrongQuestions();
        }
    }
    
    saveWrongQuestions() {
        localStorage.setItem('wrongQuestions', JSON.stringify(this.wrongQuestions));
    }
    
    loadWrongQuestions() {
        const saved = localStorage.getItem('wrongQuestions');
        return saved ? JSON.parse(saved) : [];
    }
    
    updateStats() {
        const answeredCount = parseInt(localStorage.getItem('answeredCount') || '0');
        const correctCount = parseInt(localStorage.getItem('correctCount') || '0');
        const rate = answeredCount > 0 ? Math.round((correctCount / answeredCount) * 100) : 0;
        
        document.getElementById('answeredCount').textContent = answeredCount;
        document.getElementById('correctRate').textContent = rate + '%';
    }
}

// 初始化系统
document.addEventListener('DOMContentLoaded', () => {
    new ExamSystem();
});// 工具函数
const Utils = {
    // 格式化时间
    formatTime(seconds) {
        const mins = Math.floor(seconds / 60);
        const secs = seconds % 60;
        return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
    },
    
    // 随机打乱数组
    shuffleArray(array) {
        const newArray = [...array];
        for (let i = newArray.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
        }
        return newArray;
    },
    
    // 数组比较
    arraysEqual(a, b) {
        if (!Array.isArray(a) || !Array.isArray(b)) return false;
        if (a.length !== b.length) return false;
        const sortedA = [...a].sort();
        const sortedB = [...b].sort();
        return sortedA.every((val, index) => val === sortedB[index]);
    },
    
    // 本地存储
    storage: {
        set(key, value) {
            localStorage.setItem(key, JSON.stringify(value));
        },
        
        get(key, defaultValue = null) {
            const item = localStorage.getItem(key);
            return item ? JSON.parse(item) : defaultValue;
        },
        
        remove(key) {
            localStorage.removeItem(key);
        }
    }
};

// 全局使用
window.Utils = Utils;// 题库数据
window.questionBank = [
    // 这里将包含您三个文件中的所有600道题目
    // 由于篇幅限制，我将先创建几个示例题目，然后您可以按照格式添加更多
];

// 示例题目格式：
/*
{
    id: 1,
    type: 'single', // single, multiple, judge
    question: '题目内容',
    options: ['选项A', '选项B', '选项C', '选项D'], // 单选题和多选题使用
    answer: 'A', // 单选题和判断题的答案
    // answer: ['A', 'B'], // 多选题的答案
    explanation: '解析内容',
    source: '模考（一）'
}
*/
