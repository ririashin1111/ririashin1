<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>표제음악 비밀 탐험 테스트</title>
    <style>
        body {
            font-family: 'Comic Sans MS', cursive, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .title {
            text-align: center;
            color: white;
            font-size: 2.5em;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            animation: glow 2s ease-in-out infinite alternate;
        }
        
        @keyframes glow {
            from { text-shadow: 2px 2px 4px rgba(0,0,0,0.5), 0 0 20px rgba(255,255,255,0.3); }
            to { text-shadow: 2px 2px 4px rgba(0,0,0,0.5), 0 0 30px rgba(255,255,255,0.6); }
        }
        
        .subtitle {
            text-align: center;
            color: white;
            font-size: 1.3em;
            margin-bottom: 30px;
            opacity: 0.9;
        }
        
        .instruction {
            text-align: center;
            background: rgba(255, 255, 255, 0.95);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 30px;
            font-size: 1.1em;
            color: #333;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            border: 2px solid rgba(255,255,255,0.3);
        }
        
        .songs-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }
        
        .song-button {
            background: linear-gradient(145deg, #ffffff, #f0f0f0);
            border: 3px solid #ddd;
            border-radius: 15px;
            padding: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            position: relative;
            overflow: hidden;
            min-height: 120px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        
        .song-button:hover {
            transform: translateY(-3px) scale(1.02);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            border-color: #667eea;
        }
        
        .song-button.revealed {
            background: linear-gradient(145deg, #4ecdc4, #44a08d);
            color: white;
            border-color: #4ecdc4;
            box-shadow: 0 10px 25px rgba(78, 205, 196, 0.3);
        }
        
        .song-button.clicked {
            transform: scale(0.95);
        }
        
        .song-number {
            font-size: 2.5em;
            font-weight: bold;
            margin-bottom: 10px;
            color: #667eea;
        }
        
        .song-button.revealed .song-number {
            color: white;
        }
        
        .song-label {
            font-size: 1.1em;
            font-weight: bold;
            opacity: 0.8;
        }
        
        .mystery-icon {
            font-size: 1.5em;
            margin-top: 10px;
        }
        
        .revealed-info {
            display: none;
            margin-top: 10px;
        }
        
        .song-button.revealed .mystery-icon {
            display: none;
        }
        
        .song-button.revealed .revealed-info {
            display: block;
        }
        
        .composer-name {
            font-size: 0.9em;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .song-title {
            font-size: 0.8em;
            opacity: 0.9;
        }
        
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            display: none;
            z-index: 1000;
            animation: fadeIn 0.3s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .modal-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            border-radius: 25px;
            padding: 35px;
            max-width: 700px;
            max-height: 85vh;
            overflow-y: auto;
            animation: bounceIn 0.5s ease;
            box-shadow: 0 25px 50px rgba(0,0,0,0.4);
            border: 3px solid #4ecdc4;
        }
        
        @keyframes bounceIn {
            0% { transform: translate(-50%, -50%) scale(0.3); opacity: 0; }
            50% { transform: translate(-50%, -50%) scale(1.05); }
            70% { transform: translate(-50%, -50%) scale(0.9); }
            100% { transform: translate(-50%, -50%) scale(1); opacity: 1; }
        }
        
        .close-btn {
            position: absolute;
            top: 15px;
            right: 20px;
            background: #ff4757;
            color: white;
            border: none;
            border-radius: 50%;
            width: 45px;
            height: 45px;
            cursor: pointer;
            font-size: 1.3em;
            transition: all 0.3s ease;
            font-weight: bold;
        }
        
        .close-btn:hover {
            background: #ff3838;
            transform: scale(1.1) rotate(90deg);
        }
        
        .modal-header {
            text-align: center;
            margin-bottom: 25px;
            border-bottom: 3px solid #4ecdc4;
            padding-bottom: 20px;
        }
        
        .modal-emoji {
            font-size: 4em;
            margin-bottom: 15px;
            animation: spin 3s ease-in-out infinite;
        }
        
        @keyframes spin {
            0%, 100% { transform: rotate(0deg) scale(1); }
            25% { transform: rotate(-5deg) scale(1.1); }
            75% { transform: rotate(5deg) scale(1.1); }
        }
        
        .modal-song-title {
            font-size: 2em;
            font-weight: bold;
            color: #333;
            margin-bottom: 10px;
        }
        
        .modal-composer {
            font-size: 1.3em;
            color: #4ecdc4;
            font-weight: bold;
        }
        
        .info-section {
            margin-bottom: 25px;
        }
        
        .section-title {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            color: white;
            padding: 12px 18px;
            border-radius: 12px;
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 1.1em;
        }
        
        .section-content {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 12px;
            border-left: 4px solid #4ecdc4;
            line-height: 1.6;
            font-size: 1.05em;
        }
        
        .composer-info {
            background: linear-gradient(145deg, #e8f5e8, #d4f1d4);
            padding: 15px;
            border-radius: 10px;
            margin: 10px 0;
            border-left: 4px solid #4caf50;
        }
        
        .score-display {
            text-align: center;
            background: linear-gradient(145deg, #ffffff, #f0f0f0);
            border-radius: 20px;
            padding: 25px;
            margin-top: 30px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.1);
            border: 2px solid rgba(78, 205, 196, 0.3);
        }
        
        .score-title {
            font-size: 1.4em;
            font-weight: bold;
            margin-bottom: 15px;
            color: #333;
        }
        
        .score-number {
            font-size: 3.5em;
            font-weight: bold;
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }
        
        .progress-bar {
            width: 100%;
            height: 20px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin: 20px 0;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4ecdc4, #44a08d);
            width: 0%;
            transition: width 0.5s ease;
            border-radius: 10px;
        }
        
        .reset-btn {
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            margin-top: 15px;
            font-weight: bold;
            font-size: 1.1em;
            transition: all 0.3s ease;
        }
        
        .reset-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(255, 107, 107, 0.4);
        }
        
        .completion-message {
            display: none;
            background: linear-gradient(145deg, #4ecdc4, #44a08d);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-top: 20px;
            text-align: center;
            font-size: 1.2em;
            font-weight: bold;
            animation: celebrate 1s ease;
        }
        
        @keyframes celebrate {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        
        @media (max-width: 768px) {
            .songs-grid {
                grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
                gap: 10px;
            }
            
            .song-button {
                padding: 20px;
                min-height: 100px;
            }
            
            .song-number {
                font-size: 2em;
            }
            
            .modal-content {
                max-width: 95%;
                padding: 25px;
            }
            
            .modal-emoji {
                font-size: 3em;
            }
            
            .modal-song-title {
                font-size: 1.5em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="title">🔍 표제음악 비밀 탐험 🎵</h1>
        <div class="subtitle">10개의 신비로운 곡들의 정체를 밝혀보세요!</div>
        
        <div class="instruction">
            <strong>🕵️‍♂️ 탐험 방법</strong><br>
            각 곡 번호를 클릭하면 숨겨진 작곡가와 곡 제목이 공개됩니다!<br>
            모든 비밀을 풀어보세요 ✨
        </div>
        
        <div class="songs-grid">
            <div class="song-button" data-song="1">
                <div class="song-number">1</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🎭</div>
                <div class="revealed-info">
                    <div class="composer-name">차이코프스키</div>
                    <div class="song-title">사탕요정의 춤</div>
                </div>
            </div>
            
            <div class="song-button" data-song="2">
                <div class="song-number">2</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🌟</div>
                <div class="revealed-info">
                    <div class="composer-name">홀스트</div>
                    <div class="song-title">금성</div>
                </div>
            </div>
            
            <div class="song-button" data-song="3">
                <div class="song-number">3</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🦢</div>
                <div class="revealed-info">
                    <div class="composer-name">차이코프스키</div>
                    <div class="song-title">백조의 호수</div>
                </div>
            </div>
            
            <div class="song-button" data-song="4">
                <div class="song-number">4</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">⚔️</div>
                <div class="revealed-info">
                    <div class="composer-name">홀스트</div>
                    <div class="song-title">화성</div>
                </div>
            </div>
            
            <div class="song-button" data-song="5">
                <div class="song-number">5</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🐺</div>
                <div class="revealed-info">
                    <div class="composer-name">프로코피예프</div>
                    <div class="song-title">피터와 늑대 중 피터</div>
                </div>
            </div>
            
            <div class="song-button" data-song="6">
                <div class="song-number">6</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🪐</div>
                <div class="revealed-info">
                    <div class="composer-name">홀스트</div>
                    <div class="song-title">천왕성</div>
                </div>
            </div>
            
            <div class="song-button" data-song="7">
                <div class="song-number">7</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🏹</div>
                <div class="revealed-info">
                    <div class="composer-name">로시니</div>
                    <div class="song-title">빌헬름 텔 서곡</div>
                </div>
            </div>
            
            <div class="song-button" data-song="8">
                <div class="song-number">8</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🌟</div>
                <div class="revealed-info">
                    <div class="composer-name">홀스트</div>
                    <div class="song-title">목성</div>
                </div>
            </div>
            
            <div class="song-button" data-song="9">
                <div class="song-number">9</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🇷🇺</div>
                <div class="revealed-info">
                    <div class="composer-name">차이코프스키</div>
                    <div class="song-title">러시아 행진곡</div>
                </div>
            </div>
            
            <div class="song-button" data-song="10">
                <div class="song-number">10</div>
                <div class="song-label">번 곡</div>
                <div class="mystery-icon">🌊</div>
                <div class="revealed-info">
                    <div class="composer-name">홀스트</div>
                    <div class="song-title">해왕성</div>
                </div>
            </div>
        </div>
        
        <div class="score-display">
            <div class="score-title">🏆 발견한 곡</div>
            <div class="score-number"><span id="score">0</span> / 10</div>
            <div class="progress-bar">
                <div class="progress-fill" id="progress"></div>
            </div>
            <button class="reset-btn" onclick="resetProgress()">🔄 다시 탐험하기</button>
            <div class="completion-message" id="completion">
                🎉 축하합니다! 모든 비밀을 밝혀냈습니다! 🎉<br>
                표제음악의 신비로운 세계를 모두 탐험했어요!
            </div>
        </div>
    </div>
    
    <!-- 모달들 -->
    <!-- 1번 곡 모달 -->
    <div class="modal" id="modal-1">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">🧚‍♀️</div>
                <div class="modal-song-title">사탕요정의 춤</div>
                <div class="modal-composer">차이코프스키 (1840-1893)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>러시아의 대표적인 발레 음악가</strong><br>
                        차이코프스키는 러시아가 낳은 위대한 작곡가로, 특히 발레 음악 분야에서 독보적인 위치를 차지하고 있습니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    이 곡은 발레 <strong>"호두까기 인형"</strong>에서 나온 곡입니다.<br><br>
                    <strong>🎼 특별한 악기:</strong> 첼레스타(Celesta)라는 신비로운 악기가 사용되었어요. 이 악기는 종소리와 비슷하면서도 더욱 부드러운 소리를 냅니다.<br><br>
                    <strong>✨ 음악적 표현:</strong> 사탕요정이 우아하고 환상적으로 춤추는 모습을 표현했습니다. 마치 반짝이는 별가루가 흩날리는 것 같은 신비로운 분위기를 자아내요.
                </div>
            </div>
        </div>
    </div>
    
    <!-- 2번 곡 모달 -->
    <div class="modal" id="modal-2">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">💖</div>
                <div class="modal-song-title">금성 (Venus)</div>
                <div class="modal-composer">홀스트 (1874-1934)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>영국의 우주 음악 개척자</strong><br>
                        홀스트는 천체와 우주에 매료되어 "행성" 모음곡을 작곡한 영국의 작곡가입니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>🌟 부제:</strong> "평화를 가져다주는 자" (The Bringer of Peace)<br><br>
                    <strong>💕 사랑의 행성:</strong> 금성은 로마 신화에서 사랑과 미의 여신 비너스를 상징합니다.<br><br>
                    <strong>🎼 음악적 표현:</strong> 부드럽고 아름다운 멜로디로 사랑의 따뜻함과 평화로운 감정을 표현했습니다. 현악기의 아름다운 선율이 인상적이에요.
                </div>
            </div>
        </div>
    </div>
    
    <!-- 3번 곡 모달 -->
    <div class="modal" id="modal-3">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">🦢</div>
                <div class="modal-song-title">백조의 호수</div>
                <div class="modal-composer">차이코프스키 (1840-1893)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>발레 음악의 황제</strong><br>
                        차이코프스키의 3대 발레 작품(백조의 호수, 호두까기 인형, 잠자는 숲속의 미녀) 중 가장 유명한 작품입니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>📖 스토리:</strong> 마법에 걸려 백조로 변한 오데트 공주의 슬프고 아름다운 사랑 이야기<br><br>
                    <strong>🎭 유명한 장면:</strong> 백조들이 호수에서 우아하게 춤추는 장면을 표현한 음악<br><br>
                    <strong>🎼 음악적 표현:</strong> 백조의 우아함과 공주의 슬픔을 동시에 표현한 서정적이고 아름다운 멜로디가 특징입니다.
                </div>
            </div>
        </div>
    </div>
    
    <!-- 4번 곡 모달 -->
    <div class="modal" id="modal-4">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">⚔️</div>
                <div class="modal-song-title">화성 (Mars)</div>
                <div class="modal-composer">홀스트 (1874-1934)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>행성 시리즈의 대가</strong><br>
                        홀스트의 "행성" 모음곡 중 가장 강렬하고 인상적인 곡으로, 많은 영화 음악에 영감을 주었습니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>⚡ 부제:</strong> "전쟁을 가져다주는 자" (The Bringer of War)<br><br>
                    <strong>🥁 특징적 리듬:</strong> 5/4박자의 독특한 리듬이 긴장감과 불안감을 조성합니다.<br><br>
                    <strong>🎼 음악적 표현:</strong> 강렬하고 무서운 리듬으로 전쟁의 공포와 파괴력을 생생하게 표현했습니다. 마치 전쟁터의 상황을 음악으로 그려낸 것 같아요.
                </div>
            </div>
        </div>
    </div>
    
    <!-- 5번 곡 모달 -->
    <div class="modal" id="modal-5">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">🦸‍♂️</div>
                <div class="modal-song-title">피터와 늑대 중 피터</div>
                <div class="modal-composer">프로코피예프 (1891-1953)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>어린이를 위한 음악 교육가</strong><br>
                        프로코피예프는 아이들에게 오케스트라 악기를 소개하기 위해 이 음악 동화를 작곡했습니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>🎼 음악 동화:</strong> 각 등장인물마다 다른 악기로 표현한 교육적 작품<br><br>
                    <strong>🎻 피터의 악기:</strong> 현악기(바이올린 등)로 용감하고 활기찬 소년 피터를 표현<br><br>
                    <strong>📚 교육적 효과:</strong> 음악만 들어도 어떤 등장인물이 나오는지 알 수 있도록 만든 혁신적인 작품입니다. 피터의 테마는 밝고 경쾌하여 용감한 소년의 모습을 잘 보여줘요.
                </div>
            </div>
        </div>
    </div>
    
    <!-- 6번 곡 모달 -->
    <div class="modal" id="modal-6">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">🪐</div>
                <div class="modal-song-title">천왕성 (Uranus)</div>
                <div class="modal-composer">홀스트 (1874-1934)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>우주의 신비를 음악으로 표현한 작곡가</strong><br>
                        홀스트는 각 행성의 특징을 독창적인 음악으로 표현했습니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>🎭 부제:</strong> "마법사" (The Magician)<br><br>
                    <strong>🔮 신비로운 분위기:</strong> 천왕성은 태양계에서 가장 추운 행성 중 하나로, 신비롭고 기괴한 특성을 가지고 있습니다.<br><br>
                    <strong>🎼 음악적 표현:</strong> 예측불가능한 리듬과 신비로운 소리들로 우주의 미지의 세계와 마법 같은 신비로움을 표현했습니다. 마치 우주 저편에서 들려오는 신비한 소리 같아요.
                </div>
            </div>
        </div>
    </div>
    
    <!-- 7번 곡 모달 -->
    <div class="modal" id="modal-7">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">🏹</div>
                <div class="modal-song-title">빌헬름 텔 서곡</div>
                <div class="modal-composer">로시니 (1792-1868)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>이탈리아의 오페라 거장</strong><br>
                        로시니는 39세에 오페라 작곡을 그만둘 만큼 천재적인 작곡가였습니다. 빠르고 정확한 작곡으로 유명했어요.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>🎪 오페라 서곡:</strong> 스위스의 영웅 빌헬름 텔의 이야기를 담은 오페라의 시작 음악<br><br>
                    <strong>🍎 유명한 장면:</strong> 활 쏘기의 명인인 텔이 아들 머리 위의 사과를 화살로 맞추는 전설적인 장면을 떠올리게 합니다.<br><br>
                    <strong>🎼 음악적 표현:</strong> 처음에는 조용하고 신비로운 분위기로 시작하다가, 점점 빨라지면서 마지막에는 매우 빠르고 신나는 멜로디로 마무리됩니다. 많은 사람들이 들어본 익숙한 멜로디예요!
                </div>
            </div>
        </div>
    </div>
    
    <!-- 8번 곡 모달 -->
    <div class="modal" id="modal-8">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">🌟</div>
                <div class="modal-song-title">목성 (Jupiter)</div>
                <div class="modal-composer">홀스트 (1874-1934)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>홀스트가 가장 사랑한 작품</strong><br>
                        "행성" 모음곡 중에서도 홀스트 자신이 가장 아끼고 사랑했던 곡입니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>🎉 부제:</strong> "즐거움을 가져다주는 자" (The Bringer of Jollity)<br><br>
                    <strong>👑 신들의 왕:</strong> 목성은 로마 신화에서 신들의 왕 주피터를 상징합니다.<br><br>
                    <strong>🎼 음악적 표현:</strong> 웅장하고 장엄한 멜로디가 특징으로, 특히 중간 부분의 아름다운 선율은 나중에 "나는 맹세하노"라는 애국가로도 사용되었습니다. 기쁨과 환희, 그리고 장엄함을 모두 담고 있어요.
                </div>
            </div>
        </div>
    </div>
    
    <!-- 9번 곡 모달 -->
    <div class="modal" id="modal-9">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">🇷🇺</div>
                <div class="modal-song-title">러시아 행진곡</div>
                <div class="modal-composer">차이코프스키 (1840-1893)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>러시아 정서를 음악으로 담은 대가</strong><br>
                        차이코프스키는 러시아의 전통적인 선율과 정서를 서양의 오케스트라 음악에 훌륭히 접목시킨 작곡가입니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>🎭 출처:</strong> 발레 "호두까기 인형" 2막에서 나오는 각국의 춤 중 하나<br><br>
                    <strong>💃 러시아 전통 춤:</strong> 러시아의 전통적인 민속 춤인 트레파크(Trepak)를 바탕으로 한 곡<br><br>
                    <strong>🎼 음악적 표현:</strong> 빠른 템포와 강렬한 리듬으로 러시아 사람들의 역동적이고 열정적인 춤을 표현했습니다. 점점 빨라지면서 흥미진진한 분위기를 만들어내요!
                </div>
            </div>
        </div>
    </div>
    
    <!-- 10번 곡 모달 -->
    <div class="modal" id="modal-10">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header">
                <div class="modal-emoji">🌊</div>
                <div class="modal-song-title">해왕성 (Neptune)</div>
                <div class="modal-composer">홀스트 (1874-1934)</div>
            </div>
            
            <div class="info-section">
                <div class="section-title">👨‍🎼 작곡가 소개</div>
                <div class="section-content">
                    <div class="composer-info">
                        <strong>"행성" 모음곡의 마지막 여행</strong><br>
                        홀스트는 해왕성으로 우주 여행의 마지막을 신비롭게 마무리했습니다.
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="section-title">🎵 곡 특징</div>
                <div class="section-content">
                    <strong>🔮 부제:</strong> "신비주의자" (The Mystic)<br><br>
                    <strong>🌌 먼 우주의 끝:</strong> 태양계 가장 바깥쪽 행성으로, 신비롭고 알 수 없는 세계를 상징<br><br>
                    <strong>🎼 음악적 표현:</strong> 여성 합창이 무대 뒤에서 "아~" 소리를 내며 마치 우주 저 멀리서 들려오는 것 같은 몽환적이고 신비로운 분위기를 연출합니다. 곡이 끝날 때는 점점 사라지며 무한한 우주 속으로 여행을 떠나는 느낌을 줍니다.
                </div>
            </div>
        </div>
    </div>

    <script>
        let revealedSongs = new Set();
        
        // 곡 버튼 클릭 이벤트
        document.querySelectorAll('.song-button').forEach(button => {
            button.addEventListener('click', function() {
                const songNumber = this.getAttribute('data-song');
                revealSong(songNumber);
                openModal(songNumber);
                
                // 클릭 애니메이션
                this.classList.add('clicked');
                setTimeout(() => {
                    this.classList.remove('clicked');
                }, 200);
            });
        });
        
        // 곡 정보 공개
        function revealSong(songNumber) {
            const button = document.querySelector(`[data-song="${songNumber}"]`);
            if (!button.classList.contains('revealed')) {
                button.classList.add('revealed');
                revealedSongs.add(songNumber);
                updateScore();
            }
        }
        
        // 모달 열기
        function openModal(songNumber) {
            document.getElementById(`modal-${songNumber}`).style.display = 'block';
        }
        
        // 모달 닫기
        function closeModal() {
            document.querySelectorAll('.modal').forEach(modal => {
                modal.style.display = 'none';
            });
        }
        
        // 모달 배경 클릭시 닫기
        document.querySelectorAll('.modal').forEach(modal => {
            modal.addEventListener('click', function(e) {
                if (e.target === this) {
                    closeModal();
                }
            });
        });
        
        // 점수 업데이트
        function updateScore() {
            const score = revealedSongs.size;
            document.getElementById('score').textContent = score;
            
            // 진행바 업데이트
            const progress = (score / 10) * 100;
            document.getElementById('progress').style.width = progress + '%';
            
            // 완주시 축하 메시지
            if (score === 10) {
                setTimeout(() => {
                    document.getElementById('completion').style.display = 'block';
                    // 축하 효과
                    confetti();
                }, 500);
            }
        }
        
        // 진행도 초기화
        function resetProgress() {
            revealedSongs.clear();
            updateScore();
            document.querySelectorAll('.song-button').forEach(button => {
                button.classList.remove('revealed');
            });
            document.getElementById('completion').style.display = 'none';
        }
        
        // 간단한 축하 효과 (콘페티 흉내)
        function confetti() {
            const colors = ['🎉', '🎊', '✨', '🌟', '💫'];
            for (let i = 0; i < 50; i++) {
                setTimeout(() => {
                    const confettiElement = document.createElement('div');
                    confettiElement.innerHTML = colors[Math.floor(Math.random() * colors.length)];
                    confettiElement.style.position = 'fixed';
                    confettiElement.style.left = Math.random() * 100 + '%';
                    confettiElement.style.top = '-10px';
                    confettiElement.style.fontSize = '20px';
                    confettiElement.style.zIndex = '9999';
                    confettiElement.style.pointerEvents = 'none';
                    document.body.appendChild(confettiElement);
                    
                    // 떨어지는 애니메이션
                    let position = -10;
                    const fall = setInterval(() => {
                        position += 5;
                        confettiElement.style.top = position + 'px';
                        if (position > window.innerHeight) {
                            clearInterval(fall);
                            document.body.removeChild(confettiElement);
                        }
                    }, 50);
                }, i * 100);
            }
        }
        
        // ESC 키로 모달 닫기
        document.addEventListener('keydown', function(e) {
            if (e.key === 'Escape') {
                closeModal();
            }
        });
    </script>
</body>
</html>
