<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Agente Lógico de Inteligência Artificial</title>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/qna"></script>
<style>
    #chat-container {
        width: 300px;
        margin: 0 auto;
        padding: 20px;
        border: 1px solid #ccc;
        border-radius: 5px;
        background-color: #f9f9f9;
    }
    #chat-box {
        height: 300px;
        overflow-y: scroll;
    }
    #user-input {
        width: calc(100% - 40px);
    }
</style>
</head>
<body>

<div id="chat-container">
    <div id="chat-box"></div>
    <input type="text" id="user-input" placeholder="Digite sua pergunta...">
    <button onclick="askQuestion()">Perguntar</button>
</div>

<script>
    let modelPromise;

   
    async function loadModel() {
        modelPromise = qna.load();
        await modelPromise;
    }

   
    async function respondToQuestion(question) {
        const model = await modelPromise;
        const answers = await model.findAnswers(question);
        return answers;
    }

    
    function displayMessage(sender, message) {
        var chatBox = document.getElementById("chat-box");
        var messageElement = document.createElement("div");
        messageElement.innerHTML = "<strong>" + sender + "</strong>: " + message;
        chatBox.appendChild(messageElement);
        chatBox.scrollTop = chatBox.scrollHeight;
    }

    
    async function askQuestion() {
        var question = document.getElementById("user-input").value;
        if (question.trim() !== "") {
            displayMessage("Você:", question);
            const answers = await respondToQuestion(question);
            if (answers && answers.length > 0) {
                displayMessage("Agente de IA:", answers[0].text);
            } else {
                displayMessage("Agente de IA:", "Desculpe, não encontrei uma resposta para essa pergunta



