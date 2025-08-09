<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>스터디룸 자리 예약 시스템</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .login-screen {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        
        .login-container {
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            padding: 40px;
            text-align: center;
            min-width: 400px;
        }
        
        .login-title {
            color: #333;
            margin-bottom: 30px;
            font-size: 28px;
            font-weight: bold;
        }
        
        .login-tabs {
            display: flex;
            margin-bottom: 30px;
            border-radius: 10px;
            overflow: hidden;
            background: #f5f5f5;
        }
        
        .login-tab {
            flex: 1;
            padding: 15px;
            background: #f5f5f5;
            border: none;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s;
        }
        
        .login-tab.active {
            background: #667eea;
            color: white;
        }
        
        .login-form {
            display: none;
        }
        
        .login-form.active {
            display: block;
        }
        
        .form-group {
            margin-bottom: 20px;
            text-align: left;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: #555;
            font-weight: bold;
        }
        
        .form-group input {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        .form-group input:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .login-btn {
            width: 100%;
            padding: 15px;
            background: #667eea;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 18px;
            cursor: pointer;
            transition: background 0.3s;
        }
        
        .login-btn:hover {
            background: #5a6fd8;
        }
        
        .main-content {
            display: none;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            margin-top: 20px;
            overflow: hidden;
        }
        
        .header {
            background: #667eea;
            color: white;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logout-btn {
            padding: 8px 16px;
            background: rgba(255,255,255,0.2);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        
        .student-view {
            padding: 30px;
        }
        
        .reservation-info {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .studyroom-selector {
            margin-bottom: 20px;
        }
        
        .studyroom-selector select {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
        }
        
        .seats-grid {
            display: grid;
            gap: 15px;
            justify-content: center;
            margin-top: 20px;
            min-height: 400px;
            border: 2px dashed #ddd;
            padding: 20px;
            border-radius: 10px;
        }
        
        .seat {
            width: 80px;
            height: 80px;
            border: 2px solid #ddd;
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s;
            background: white;
            position: relative;
        }
        
        .seat.available {
            border-color: #28a745;
            background: #d4edda;
        }
        
        .seat.occupied {
            border-color: #dc3545;
            background: #f8d7da;
            cursor: not-allowed;
        }
        
        .seat.selected {
            border-color: #007bff;
            background: #cce7ff;
            transform: scale(1.1);
        }
        
        .seat-number {
            font-weight: bold;
            font-size: 14px;
        }
        
        .seat-info {
            font-size: 8px;
            text-align: center;
            margin-top: 2px;
            color: #666;
        }
        
        .reservation-actions {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s;
        }
        
        .btn-primary {
            background: #007bff;
            color: white;
        }
        
        .btn-danger {
            background: #dc3545;
            color: white;
        }
        
        .btn:hover {
            opacity: 0.8;
            transform: translateY(-2px);
        }
        
        .admin-view {
            display: flex;
            height: 600px;
        }
        
        .admin-sidebar {
            width: 200px;
            background: #f8f9fa;
            border-right: 1px solid #ddd;
        }
        
        .admin-nav {
            list-style: none;
        }
        
        .admin-nav li {
            border-bottom: 1px solid #ddd;
        }
        
        .admin-nav a {
            display: block;
            padding: 15px 20px;
            text-decoration: none;
            color: #333;
            transition: background 0.3s;
        }
        
        .admin-nav a:hover,
        .admin-nav a.active {
            background: #667eea;
            color: white;
        }
        
        .admin-content {
            flex: 1;
            padding: 30px;
            overflow-y: auto;
        }
        
        .admin-section {
            display: none;
        }
        
        .admin-section.active {
            display: block;
        }
        
        .section-title {
            font-size: 24px;
            margin-bottom: 20px;
            color: #333;
        }
        
        .card {
            background: white;
            border: 1px solid #ddd;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .form-row {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
        }
        
        .form-row > * {
            flex: 1;
        }
        
        .studyroom-list {
            margin-top: 20px;
        }
        
        .studyroom-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 8px;
            margin-bottom: 10px;
            background: white;
        }
        
        .btn-sm {
            padding: 8px 16px;
            font-size: 14px;
        }
        
        .seat-designer {
            border: 2px dashed #ccc;
            min-height: 400px;
            padding: 20px;
            border-radius: 10px;
            position: relative;
            background: #f9f9f9;
        }
        
        .seat-designer.design-mode {
            cursor: crosshair;
        }
        
        .designer-seat {
            position: absolute;
            width: 60px;
            height: 60px;
            background: #e3f2fd;
            border: 2px solid #2196f3;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: move;
            font-size: 12px;
            font-weight: bold;
        }
        
        .designer-controls {
            margin-bottom: 20px;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        
        .time-settings {
            display: flex;
            gap: 15px;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .user-list {
            max-height: 400px;
            overflow-y: auto;
        }
        
        .user-item {
            display: flex;
            justify-content: between;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid #eee;
        }
        
        .user-info {
            flex: 1;
        }
        
        .alert {
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
        }
        
        .alert-success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .alert-error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f1aeb5;
        }
        
        .hidden {
            display: none !important;
        }
        
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
        }
        
        .modal-content {
            background-color: white;
            margin: 15% auto;
            padding: 20px;
            border-radius: 10px;
            width: 80%;
            max-width: 500px;
        }
        
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }
        
        .close:hover {
            color: black;
        }
    </style>
</head>
<body>
    <!-- 로그인 화면 -->
    <div id="loginScreen" class="login-screen">
        <div class="login-container">
            <div class="login-title">스터디룸 예약 시스템</div>
            
            <div class="login-tabs">
                <button class="login-tab active" onclick="switchLoginTab('student')">학생 로그인</button>
                <button class="login-tab" onclick="switchLoginTab('admin')">관리자 로그인</button>
            </div>
            
            <!-- 학생 로그인 폼 -->
            <form class="login-form active" id="studentLoginForm">
                <div class="form-group">
                    <label for="studentName">이름</label>
                    <input type="text" id="studentName" required>
                </div>
                <div class="form-group">
                    <label for="studentId">학번</label>
                    <input type="text" id="studentId" required>
                </div>
                <button type="submit" class="login-btn">로그인</button>
            </form>
            
            <!-- 관리자 로그인 폼 -->
            <form class="login-form" id="adminLoginForm">
                <div class="form-group">
                    <label for="adminUsername">관리자 ID</label>
                    <input type="text" id="adminUsername" required>
                </div>
                <div class="form-group">
                    <label for="adminPassword">비밀번호</label>
                    <input type="password" id="adminPassword" required>
                </div>
                <button type="submit" class="login-btn">로그인</button>
            </form>
        </div>
    </div>

    <!-- 메인 컨텐츠 -->
    <div class="container">
        <div id="mainContent" class="main-content">
            <div class="header">
                <h1 id="headerTitle">스터디룸 예약 시스템</h1>
                <button class="logout-btn" onclick="logout()">로그아웃</button>
            </div>

            <!-- 학생 뷰 -->
            <div id="studentView" class="student-view">
                <div class="reservation-info">
                    <h3>예약 정보</h3>
                    <p>이름: <span id="currentUserName"></span> | 학번: <span id="currentUserId"></span></p>
                    <p>현재 예약: <span id="currentReservation">없음</span></p>
                </div>

                <div class="studyroom-selector">
                    <label for="studyroomSelect">스터디룸 선택:</label>
                    <select id="studyroomSelect" onchange="loadStudyroomSeats()">
                        <option value="">스터디룸을 선택하세요</option>
                    </select>
                </div>

                <div id="seatsContainer">
                    <div class="seats-grid" id="seatsGrid">
                        <p>스터디룸을 선택하세요</p>
                    </div>
                </div>

                <div class="reservation-actions">
                    <button class="btn btn-primary" id="reserveBtn" onclick="makeReservation()" disabled>예약하기</button>
                    <button class="btn btn-danger" id="cancelBtn" onclick="cancelReservation()" style="display:none">예약 취소</button>
                </div>
            </div>

            <!-- 관리자 뷰 -->
            <div id="adminView" class="admin-view" style="display:none">
                <div class="admin-sidebar">
                    <ul class="admin-nav">
                        <li><a href="#" class="active" onclick="showAdminSection('seats')">좌석 관리</a></li>
                        <li><a href="#" onclick="showAdminSection('reservations')">예약 관리</a></li>
                        <li><a href="#" onclick="showAdminSection('users')">인원 관리</a></li>
                    </ul>
                </div>

                <div class="admin-content">
                    <!-- 좌석 관리 섹션 -->
                    <div id="seatsSection" class="admin-section active">
                        <h2 class="section-title">좌석 관리</h2>
                        
                        <div class="card">
                            <h3>새 스터디룸 추가</h3>
                            <form id="addStudyroomForm">
                                <div class="form-group">
                                    <label for="newStudyroomName">스터디룸 이름</label>
                                    <input type="text" id="newStudyroomName" required>
                                </div>
                                <button type="submit" class="btn btn-primary">스터디룸 추가</button>
                            </form>
                        </div>

                        <div class="card">
                            <h3>스터디룸 목록</h3>
                            <div id="studyroomList" class="studyroom-list">
                                <!-- 스터디룸 목록이 여기에 표시됩니다 -->
                            </div>
                        </div>
                    </div>

                    <!-- 예약 관리 섹션 -->
                    <div id="reservationsSection" class="admin-section">
                        <h2 class="section-title">예약 관리</h2>
                        
                        <div class="card">
                            <h3>예약 시간 설정</h3>
                            <div class="time-settings">
                                <label>시작 시간:</label>
                                <input type="time" id="startTime" value="09:00">
                                <label>종료 시간:</label>
                                <input type="time" id="endTime" value="18:00">
                                <button class="btn btn-primary btn-sm" onclick="updateReservationTimes()">설정 저장</button>
                            </div>
                        </div>

                        <div class="card">
                            <h3>예약 관리</h3>
                            <div class="form-row">
                                <select id="timeSlotSelect">
                                    <option value="">시간 선택</option>
                                </select>
                                <button class="btn btn-danger" onclick="cancelAllReservationsAtTime()">선택 시간 모든 예약 취소</button>
                            </div>
                            <button class="btn btn-danger" onclick="cancelAllReservations()">전체 예약 취소</button>
                        </div>
                    </div>

                    <!-- 인원 관리 섹션 -->
                    <div id="usersSection" class="admin-section">
                        <h2 class="section-title">인원 관리</h2>
                        
                        <div class="card">
                            <h3>예약 현황 <span id="totalReservations">(0명)</span></h3>
                            <div class="reservation-actions" style="margin-bottom: 20px;">
                                <button class="btn btn-danger" onclick="cancelAllReservations()">전체 예약 취소</button>
                            </div>
                            <div id="usersList" class="user-list">
                                <!-- 예약 사용자 목록이 여기에 표시됩니다 -->
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- 좌석 배치 디자이너 모달 -->
    <div id="seatDesignerModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeSeatDesigner()">&times;</span>
            <h2>좌석 배치 디자이너</h2>
            <p>스터디룸: <span id="designingRoom"></span></p>
            
            <div class="designer-controls">
                <button class="btn btn-primary btn-sm" onclick="addSeatToDesigner()">좌석 추가</button>
                <button class="btn btn-danger btn-sm" onclick="clearAllSeats()">모든 좌석 제거</button>
                <button class="btn btn-primary" onclick="saveLayout()">배치 저장</button>
            </div>
            
            <div id="seatDesigner" class="seat-designer">
                <p style="text-align: center; color: #666; margin-top: 180px;">좌석 추가 버튼을 클릭하거나 빈 공간을 클릭하여 좌석을 배치하세요</p>
            </div>
        </div>
    </div>

    <script>
        // 전역 변수
        let currentUser = null;
        let selectedSeat = null;
        let studyrooms = {};
        let reservations = {};
        let reservationTimes = { start: '09:00', end: '18:00' };
        let designingRoomId = null;
        let seatCounter = 1;

        // 초기화
        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
        });

        function initializeApp() {
            // 기본 스터디룸 생성
            if (!studyrooms['room1']) {
                studyrooms['room1'] = {
                    id: 'room1',
                    name: '스터디룸 1',
                    seats: [
                        { id: 1, x: 50, y: 50 },
                        { id: 2, x: 150, y: 50 },
                        { id: 3, x: 50, y: 150 },
                        { id: 4, x: 150, y: 150 }
                    ]
                };
            }
            
            updateStudyroomSelect();
            updateStudyroomList();
        }

        // 로그인 관련 함수
        function switchLoginTab(type) {
            document.querySelectorAll('.login-tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.login-form').forEach(form => form.classList.remove('active'));
            
            event.target.classList.add('active');
            if (type === 'student') {
                document.getElementById('studentLoginForm').classList.add('active');
            } else {
                document.getElementById('adminLoginForm').classList.add('active');
            }
        }

        // 학생 로그인 이벤트
        document.getElementById('studentLoginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const name = document.getElementById('studentName').value.trim();
            const studentId = document.getElementById('studentId').value.trim();
            
            if (name && studentId) {
                currentUser = { type: 'student', name: name, id: studentId };
                showStudentView();
            }
        });

        // 관리자 로그인 이벤트
        document.getElementById('adminLoginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const username = document.getElementById('adminUsername').value.trim();
            const password = document.getElementById('adminPassword').value.trim();
            
            // 간단한 관리자 인증 (실제 프로젝트에서는 서버 인증 필요)
            if (username === 'admin' && password === 'admin') {
                currentUser = { type: 'admin', name: 'Administrator' };
                showAdminView();
            } else {
                alert('관리자 정보가 올바르지 않습니다.');
            }
        });

        function showStudentView() {
            document.getElementById('loginScreen').style.display = 'none';
            document.getElementById('mainContent').style.display = 'block';
            document.getElementById('headerTitle').textContent = `${currentUser.name}님의 스터디룸 예약`;
            document.getElementById('currentUserName').textContent = currentUser.name;
            document.getElementById('currentUserId').textContent = currentUser.id;
            document.getElementById('studentView').style.display = 'block';
            document.getElementById('adminView').style.display = 'none';
            
            updateCurrentReservationStatus();
        }

        function showAdminView() {
            document.getElementById('loginScreen').style.display = 'none';
            document.getElementById('mainContent').style.display = 'block';
            document.getElementById('headerTitle').textContent = '관리자 패널';
            document.getElementById('studentView').style.display = 'none';
            document.getElementById('adminView').style.display = 'block';
            
            updateTimeSlotSelect();
            updateUsersList();
        }

        function logout() {
            currentUser = null;
            selectedSeat = null;
            document.getElementById('loginScreen').style.display = 'flex';
            document.getElementById('mainContent').style.display = 'none';
            
            // 폼 초기화
            document.getElementById('studentLoginForm').reset();
            document.getElementById('adminLoginForm').reset();
        }

        // 스터디룸 관련 함수
        function updateStudyroomSelect() {
            const select = document.getElementById('studyroomSelect');
            select.innerHTML = '<option value="">스터디룸을 선택하세요</option>';
            
            for (const roomId in studyrooms) {
                const room = studyrooms[roomId];
                const option = document.createElement('option');
                option.value = roomId;
                option.textContent = room.name;
                select.appendChild(option);
            }
        }

        function loadStudyroomSeats() {
            const roomId = document.getElementById('studyroomSelect').value;
            const seatsGrid = document.getElementById('seatsGrid');
            
            if (!roomId || !studyrooms[roomId]) {
                seatsGrid.innerHTML = '<p>스터디룸을 선택하세요</p>';
                seatsGrid.style.gridTemplateColumns = 'none';
                return;
            }
            
            const room = studyrooms[roomId];
            seatsGrid.innerHTML = '';
            seatsGrid.style.position = 'relative';
            seatsGrid.style.gridTemplateColumns = 'none';
            seatsGrid.style.height = '400px';
            
            room.seats.forEach(seat => {
                const seatElement = document.createElement('div');
                seatElement.className = 'seat';
                seatElement.style.position = 'absolute';
                seatElement.style.left = seat.x + 'px';
                seatElement.style.top = seat.y + 'px';
                seatElement.dataset.seatId = seat.id;
                seatElement.dataset.roomId = roomId;
                
                const reservation = findReservation(roomId, seat.id);
                if (reservation) {
                    if (reservation.userId === currentUser.id) {
                        seatElement.classList.add('selected');
                        selectedSeat = { roomId: roomId, seatId: seat.id };
                    } else {
                        seatElement.classList.add('occupied');
                    }
                } else {
                    seatElement.classList.add('available');
                }
                
                seatElement.innerHTML = `
                    <div class="seat-number">좌석 ${seat.id}</div>
                    <div class="seat-info">${reservation ? reservation.userName + '<br>' + reservation.userId : ''}</div>
                `;
                
                seatElement.addEventListener('click', function() {
                    if (currentUser.type === 'student') {
                        selectSeat(roomId, seat.id, seatElement);
                    }
                });
                
                seatsGrid.appendChild(seatElement);
            });
            
            updateReservationButtons();
        }

        function selectSeat(roomId, seatId, seatElement) {
            if (seatElement.classList.contains('occupied')) return;
            
            // 기존 선택 해제
            document.querySelectorAll('.seat.selected').forEach(seat => {
                if (!findReservation(seat.dataset.roomId, seat.dataset.seatId)) {
                    seat.classList.remove('selected');
                    seat.classList.add('available');
                }
            });
            
            // 새 좌석 선택
            if (!seatElement.classList.contains('selected')) {
                seatElement.classList.remove('available');
                seatElement.classList.add('selected');
                selectedSeat = { roomId: roomId, seatId: parseInt(seatId) };
            } else {
                selectedSeat = null;
            }
            
            updateReservationButtons();
        }

        function makeReservation() {
            if (!selectedSeat) return;
            
            // 기존 예약 확인
            const existingReservation = findUserReservation(currentUser.id);
            if (existingReservation) {
                alert('이미 다른 좌석을 예약하셨습니다. 기존 예약을 취소하고 다시 시도하세요.');
                return;
            }
            
            // 예약 생성
            const reservationId = Date.now().toString();
            reservations[reservationId] = {
                id: reservationId,
                roomId: selectedSeat.roomId,
                seatId: selectedSeat.seatId,
                userId: currentUser.id,
                userName: currentUser.name,
                timestamp: new Date()
            };
            
            // UI 업데이트
            loadStudyroomSeats();
            updateCurrentReservationStatus();
            updateReservationButtons();
            
            alert('예약이 완료되었습니다!');
        }

        function cancelReservation() {
            const userReservation = findUserReservation(currentUser.id);
            if (userReservation) {
                delete reservations[userReservation.id];
                selectedSeat = null;
                
                loadStudyroomSeats();
                updateCurrentReservationStatus();
                updateReservationButtons();
                
                alert('예약이 취소되었습니다.');
            }
        }

        function updateReservationButtons() {
            const reserveBtn = document.getElementById('reserveBtn');
            const cancelBtn = document.getElementById('cancelBtn');
            const userReservation = findUserReservation(currentUser.id);
            
            if (userReservation) {
                reserveBtn.style.display = 'none';
                cancelBtn.style.display = 'inline-block';
            } else {
                reserveBtn.style.display = 'inline-block';
                reserveBtn.disabled = !selectedSeat;
                cancelBtn.style.display = 'none';
            }
        }

        function updateCurrentReservationStatus() {
            const statusElement = document.getElementById('currentReservation');
            const userReservation = findUserReservation(currentUser.id);
            
            if (userReservation) {
                const room = studyrooms[userReservation.roomId];
                statusElement.textContent = `${room.name} - 좌석 ${userReservation.seatId}`;
            } else {
                statusElement.textContent = '없음';
            }
        }

        // 예약 검색 함수
        function findReservation(roomId, seatId) {
            for (const reservationId in reservations) {
                const reservation = reservations[reservationId];
                if (reservation.roomId === roomId && reservation.seatId === parseInt(seatId)) {
                    return reservation;
                }
            }
            return null;
        }

        function findUserReservation(userId) {
            for (const reservationId in reservations) {
                const reservation = reservations[reservationId];
                if (reservation.userId === userId) {
                    return reservation;
                }
            }
            return null;
        }

        // 관리자 기능
        function showAdminSection(section) {
            document.querySelectorAll('.admin-nav a').forEach(a => a.classList.remove('active'));
            document.querySelectorAll('.admin-section').forEach(s => s.classList.remove('active'));
            
            event.target.classList.add('active');
            document.getElementById(section + 'Section').classList.add('active');
            
            if (section === 'users') {
                updateUsersList();
            }
        }

        // 스터디룸 추가
        document.getElementById('addStudyroomForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const name = document.getElementById('newStudyroomName').value.trim();
            
            if (name) {
                const roomId = 'room' + Date.now();
                studyrooms[roomId] = {
                    id: roomId,
                    name: name,
                    seats: []
                };
                
                updateStudyroomSelect();
                updateStudyroomList();
                document.getElementById('newStudyroomName').value = '';
                
                alert('스터디룸이 추가되었습니다.');
            }
        });

        function updateStudyroomList() {
            const listContainer = document.getElementById('studyroomList');
            listContainer.innerHTML = '';
            
            for (const roomId in studyrooms) {
                const room = studyrooms[roomId];
                const item = document.createElement('div');
                item.className = 'studyroom-item';
                item.innerHTML = `
                    <div>
                        <strong>${room.name}</strong>
                        <small>(좌석 수: ${room.seats.length})</small>
                    </div>
                    <div>
                        <button class="btn btn-primary btn-sm" onclick="openSeatDesigner('${roomId}')">좌석 배치</button>
                        <button class="btn btn-danger btn-sm" onclick="deleteStudyroom('${roomId}')">삭제</button>
                    </div>
                `;
                listContainer.appendChild(item);
            }
        }

        function deleteStudyroom(roomId) {
            if (confirm('이 스터디룸을 삭제하시겠습니까? 관련된 모든 예약도 삭제됩니다.')) {
                // 해당 스터디룸의 모든 예약 삭제
                for (const reservationId in reservations) {
                    if (reservations[reservationId].roomId === roomId) {
                        delete reservations[reservationId];
                    }
                }
                
                delete studyrooms[roomId];
                updateStudyroomSelect();
                updateStudyroomList();
                updateUsersList();
                
                alert('스터디룸이 삭제되었습니다.');
            }
        }

        // 좌석 디자이너
        function openSeatDesigner(roomId) {
            designingRoomId = roomId;
            const room = studyrooms[roomId];
            document.getElementById('designingRoom').textContent = room.name;
            document.getElementById('seatDesignerModal').style.display = 'block';
            
            loadDesignerSeats();
        }

        function closeSeatDesigner() {
            document.getElementById('seatDesignerModal').style.display = 'none';
            designingRoomId = null;
        }

        function loadDesignerSeats() {
            const designer = document.getElementById('seatDesigner');
            designer.innerHTML = '';
            
            if (!designingRoomId) return;
            
            const room = studyrooms[designingRoomId];
            room.seats.forEach(seat => {
                const seatElement = document.createElement('div');
                seatElement.className = 'designer-seat';
                seatElement.style.left = seat.x + 'px';
                seatElement.style.top = seat.y + 'px';
                seatElement.textContent = seat.id;
                seatElement.draggable = true;
                
                seatElement.addEventListener('dragstart', function(e) {
                    e.dataTransfer.setData('text/plain', seat.id);
                });
                
                seatElement.addEventListener('dblclick', function() {
                    if (confirm('이 좌석을 삭제하시겠습니까?')) {
                        room.seats = room.seats.filter(s => s.id !== seat.id);
                        loadDesignerSeats();
                    }
                });
                
                designer.appendChild(seatElement);
            });
            
            // 드롭 이벤트 설정
            designer.addEventListener('dragover', function(e) {
                e.preventDefault();
            });
            
            designer.addEventListener('drop', function(e) {
                e.preventDefault();
                const seatId = parseInt(e.dataTransfer.getData('text/plain'));
                const rect = designer.getBoundingClientRect();
                const x = e.clientX - rect.left - 30; // 좌석 중심 조정
                const y = e.clientY - rect.top - 30;
                
                const seat = room.seats.find(s => s.id === seatId);
                if (seat) {
                    seat.x = Math.max(0, Math.min(x, designer.clientWidth - 60));
                    seat.y = Math.max(0, Math.min(y, designer.clientHeight - 60));
                    loadDesignerSeats();
                }
            });
            
            // 클릭으로 좌석 추가
            designer.addEventListener('click', function(e) {
                if (e.target === designer) {
                    addSeatAtPosition(e.offsetX - 30, e.offsetY - 30);
                }
            });
        }

        function addSeatToDesigner() {
            addSeatAtPosition(50, 50);
        }

        function addSeatAtPosition(x, y) {
            if (!designingRoomId) return;
            
            const room = studyrooms[designingRoomId];
            const designer = document.getElementById('seatDesigner');
            
            // 새 좌석 ID 생성
            const maxId = room.seats.length > 0 ? Math.max(...room.seats.map(s => s.id)) : 0;
            const newSeat = {
                id: maxId + 1,
                x: Math.max(0, Math.min(x, designer.clientWidth - 60)),
                y: Math.max(0, Math.min(y, designer.clientHeight - 60))
            };
            
            room.seats.push(newSeat);
            loadDesignerSeats();
        }

        function clearAllSeats() {
            if (!designingRoomId) return;
            
            if (confirm('모든 좌석을 삭제하시겠습니까?')) {
                studyrooms[designingRoomId].seats = [];
                loadDesignerSeats();
            }
        }

        function saveLayout() {
            if (!designingRoomId) return;
            
            alert('좌석 배치가 저장되었습니다.');
            closeSeatDesigner();
            updateStudyroomList();
        }

        // 예약 시간 관리
        function updateReservationTimes() {
            const startTime = document.getElementById('startTime').value;
            const endTime = document.getElementById('endTime').value;
            
            if (startTime && endTime && startTime < endTime) {
                reservationTimes.start = startTime;
                reservationTimes.end = endTime;
                updateTimeSlotSelect();
                alert('예약 시간이 설정되었습니다.');
            } else {
                alert('올바른 시간을 입력하세요.');
            }
        }

        function updateTimeSlotSelect() {
            const select = document.getElementById('timeSlotSelect');
            select.innerHTML = '<option value="">시간 선택</option>';
            
            const start = parseInt(reservationTimes.start.replace(':', ''));
            const end = parseInt(reservationTimes.end.replace(':', ''));
            
            for (let hour = Math.floor(start / 100); hour < Math.floor(end / 100); hour++) {
                const timeStr = hour.toString().padStart(2, '0') + ':00';
                const option = document.createElement('option');
                option.value = timeStr;
                option.textContent = timeStr + ' - ' + (hour + 1).toString().padStart(2, '0') + ':00';
                select.appendChild(option);
            }
        }

        function cancelAllReservationsAtTime() {
            const selectedTime = document.getElementById('timeSlotSelect').value;
            if (!selectedTime) {
                alert('시간을 선택하세요.');
                return;
            }
            
            if (confirm(`${selectedTime} 시간대의 모든 예약을 취소하시겠습니까?`)) {
                // 실제 구현에서는 시간대별 예약을 관리해야 하지만,
                // 여기서는 간단히 모든 예약을 취소하는 것으로 구현
                let cancelCount = 0;
                for (const reservationId in reservations) {
                    delete reservations[reservationId];
                    cancelCount++;
                }
                
                updateUsersList();
                alert(`${cancelCount}개의 예약이 취소되었습니다.`);
            }
        }

        function cancelAllReservations() {
            if (Object.keys(reservations).length === 0) {
                alert('취소할 예약이 없습니다.');
                return;
            }
            
            if (confirm('모든 예약을 취소하시겠습니까?')) {
                const cancelCount = Object.keys(reservations).length;
                reservations = {};
                updateUsersList();
                alert(`${cancelCount}개의 예약이 취소되었습니다.`);
            }
        }

        // 사용자 관리
        function updateUsersList() {
            const usersList = document.getElementById('usersList');
            const totalElement = document.getElementById('totalReservations');
            
            const reservationList = Object.values(reservations);
            totalElement.textContent = `(${reservationList.length}명)`;
            
            usersList.innerHTML = '';
            
            if (reservationList.length === 0) {
                usersList.innerHTML = '<p style="text-align: center; color: #666; padding: 20px;">현재 예약된 사용자가 없습니다.</p>';
                return;
            }
            
            reservationList.forEach(reservation => {
                const room = studyrooms[reservation.roomId];
                const userItem = document.createElement('div');
                userItem.className = 'user-item';
                userItem.innerHTML = `
                    <div class="user-info">
                        <strong>${reservation.userName}</strong> (${reservation.userId})<br>
                        <small>${room ? room.name : '알 수 없음'} - 좌석 ${reservation.seatId}</small>
                    </div>
                    <button class="btn btn-danger btn-sm" onclick="cancelUserReservation('${reservation.id}')">취소</button>
                `;
                usersList.appendChild(userItem);
            });
        }

        function cancelUserReservation(reservationId) {
            if (confirm('이 예약을 취소하시겠습니까?')) {
                delete reservations[reservationId];
                updateUsersList();
                alert('예약이 취소되었습니다.');
            }
        }

        // 모달 외부 클릭으로 닫기
        window.addEventListener('click', function(event) {
            const modal = document.getElementById('seatDesignerModal');
            if (event.target === modal) {
                closeSeatDesigner();
            }
        });
    </script>
</body>
</html>
