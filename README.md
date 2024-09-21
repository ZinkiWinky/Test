<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Permintaan Maaf Romantis</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #e6f2ff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background-color: #fff;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 400px;
        }
        h1 {
            color: #4d79ff;
        }
        p {
            color: #666;
            line-height: 1.6;
        }
        .heart {
            color: #ff4d4d;
            font-size: 50px;
            animation: pulse 1s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        .checkbox-container {
            margin: 20px 0;
            text-align: left;
        }
        .checkbox-container label {
            display: block;
            margin: 10px 0;
            cursor: pointer;
        }
        .checkbox-container input[type="checkbox"] {
            margin-right: 10px;
        }
        .button {
            background-color: #4d79ff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .button:hover {
            background-color: #3366cc;
        }
        #result {
            margin-top: 20px;
            font-weight: bold;
            color: #4d79ff;
        }
        #answerStatus {
            margin-top: 20px;
            font-weight: bold;
            color: #ff4d4d;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Maafkan Aku</h1>
        <div class="heart">&#10084;</div>
        <p>Aku tahu aku telah melakukan kesalahan. Cintaku padamu lebih besar dari apapun.</p>
        <p>Maukah kau memaafkanku dan memberi kita kesempatan lagi?</p>
        <p>Aku berjanji akan menjadi lebih baik untukmu.</p>
        <div id="answerStatus"></div>
        <div id="formContainer">
            <div class="checkbox-container">
                <label>
                    <input type="checkbox" name="forgiveness" value="yes"> Ya, aku memaafkanmu
                </label>
                <label>
                    <input type="checkbox" name="forgiveness" value="no"> Tidak, aku belum bisa memaafkanmu
                </label>
            </div>
            <button class="button" onclick="sendAnswer()">Kirim Jawaban</button>
        </div>
        <div id="result"></div>
    </div>

    <script>
        function checkAnswerStatus() {
            var status = localStorage.getItem('answerStatus');
            var answerStatusDiv = document.getElementById('answerStatus');
            var formContainer = document.getElementById('formContainer');

            if (status) {
                answerStatusDiv.innerHTML = 'Anda sudah menjawab: ' + (status === 'yes' ? 'Memaafkan' : 'Belum memaafkan');
                formContainer.style.display = 'none';
            } else {
                answerStatusDiv.innerHTML = 'Anda belum menjawab.';
            }
        }

        function sendAnswer() {
            var checkboxes = document.getElementsByName('forgiveness');
            var selected = false;
            var answer = '';
            
            for (var i = 0; i < checkboxes.length; i++) {
                if (checkboxes[i].checked) {
                    selected = true;
                    answer = checkboxes[i].value;
                    break;
                }
            }
            
            if (!selected) {
                alert('Silakan pilih salah satu opsi.');
                return;
            }

            var message = answer === 'yes' ? 
                'Terima kasih telah memaafkanku. Aku berjanji akan menjadi lebih baik.' :
                'Aku mengerti. Aku akan berusaha lebih keras untuk mendapatkan maafmu.';

            var resultDiv = document.getElementById('result');
            resultDiv.innerHTML = 'Jawaban Anda: ' + message;

            // Simpan status jawaban
            localStorage.setItem('answerStatus', answer);

            // Tampilkan konfirmasi
            setTimeout(function() {
                alert('Jawaban Anda telah berhasil disimpan.');
                checkAnswerStatus(); // Perbarui tampilan status
            }, 1000);
        }

        // Periksa status jawaban saat halaman dimuat
        window.onload = checkAnswerStatus;
    </script>
</body>
</html>
