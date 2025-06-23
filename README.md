# quote2
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1.0" />
  <title>포레테 케이터링 문의 폼</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0 16px;
      background: #f0f2f5;
      color: #333;
    }
    #catering-form {
      max-width: 720px;
      margin: 40px auto;
      background: #fff;
      padding: 32px;
      border-radius: 12px;
      box-shadow: 0 4px 16px rgba(0,0,0,0.08);
    }
    #catering-form h2 {
      text-align: center;
      font-size: 26px;
      margin-bottom: 24px;
      color: #01A081;
    }
    #catering-form label {
      display: block;
      font-weight: bold;
      margin-top: 16px;
      margin-bottom: 8px;
      font-size: 14px;
    }
    #catering-form input[type="text"],
    #catering-form input[type="number"],
    #catering-form select {
      width: 100%;
      padding: 12px;
      font-size: 14px;
      border: 1px solid #ccc;
      border-radius: 6px;
      box-sizing: border-box;
    }
    #catering-form .checkbox-group {
      display: flex;
      flex-direction: column;
      gap: 8px;
      margin-bottom: 8px;
    }
    #catering-form .checkbox-group label {
      font-weight: normal;
      display: flex;
      align-items: center;
      gap: 8px;
      cursor: pointer;
    }
    #catering-form .checkbox-group input[type="checkbox"] {
      transform: scale(1.2);
    }
    #catering-form .conditional {
      display: none;
      margin-top: 8px;
    }
    #catering-form button[type="submit"] {
      display: block;
      width: 100%;
      margin-top: 24px;
      padding: 14px;
      background: #01A081;
      color: #fff;
      font-size: 16px;
      font-weight: bold;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background 0.3s;
    }
    #catering-form button[type="submit"]:hover {
      background: #018468;
    }
    .required::after {
      content: " *";
      color: red;
    }
  </style>
</head>
<body>

<form id="catering-form">
  <h2>포레테 케이터링 문의</h2>

  <label for="expected-people" class="required">예상 인원 (1일 기준)</label>
  <input type="number" id="expected-people" name="expectedPeople" min="1" required>

  <label for="cups-per-person" class="required">잔 수 (1인당 기준)</label>
  <select id="cups-per-person" name="cupsPerPerson" required>
    <option value="" disabled selected>(선택)</option>
    <option>약 100잔</option>
    <option>약 200잔</option>
    <option>약 300잔</option>
    <option>약 400잔 이상</option>
  </select>

  <label class="required">디저트 선택 시 답변 필수</label>
  <div class="checkbox-group" id="dessert-group">
    <label><input type="checkbox" name="dessert" value="마카롱"> 마카롱 (기업 로고 각인)</label>
    <label><input type="checkbox" name="dessert" value="쿠키"> 쿠키 (기업 로고 각인)</label>
    <label>
      <input type="checkbox" id="opt-packaging" name="dessert" value="상자 포장">
      *추가 비용 옵션 선택: 상자 포장 요청
    </label>
    <div class="conditional" id="packaging-options">
      <label for="packaging-count">포장 상자 수량 선택</label>
      <select id="packaging-count" name="packagingCount">
        <option value="" disabled selected>(선택)</option>
        <option>2구</option>
        <option>3구</option>
        <option>4구</option>
      </select>
    </div>
  </div>

  <label>RTD 선택 (얼음컵 제공)</label>
  <div class="checkbox-group">
    <label><input type="checkbox" name="rtd" value="페리에 330ml *24개입"> 페리에 330ml *24개입</label>
    <label><input type="checkbox" name="rtd" value="에비앙 330ml *24개입"> 에비앙 330ml *24개입</label>
    <label><input type="checkbox" name="rtd" value="마르티넬리 골드메달 296ml *24개입"> 마르티넬리 골드메달 296ml *24개입</label>
    <label><input type="checkbox" name="rtd" value="마르티넬리 스파클링 296ml *24개입"> 마르티넬리 스파클링 296ml *24개입</label>
  </div>

  <label for="payment-method" class="required">결제 방식</label>
  <select id="payment-method" name="paymentMethod" required>
    <option value="" disabled selected>(선택)</option>
    <option>전자세금계산서 발행</option>
    <option>행사 전일 혹은 당일 현장 카드 결제</option>
  </select>

  <button type="submit">문의하기</button>
</form>

<script>
  // '상자 포장 요청' 체크 시 옵션 노출
  document.getElementById('opt-packaging').addEventListener('change', function() {
    document.getElementById('packaging-options').style.display =
      this.checked ? 'block' : 'none';
    if (!this.checked) {
      document.getElementById('packaging-count').value = '';
    }
  });

  // 폼 제출시 검증
  document.getElementById('catering-form').addEventListener('submit', function(e) {
    var dessertChecks = this.querySelectorAll('input[name="dessert"]:checked');
    var isPackagingChecked = document.getElementById('opt-packaging').checked;
    var packagingSelect = document.getElementById('packaging-count');

    // 디저트 선택 시 포장 수량 필수
    if (isPackagingChecked && !packagingSelect.value) {
      alert('상자 포장 요청 시 포장 상자 수량을 선택해 주세요.');
      packagingSelect.focus();
      e.preventDefault();
      return;
    }

    // 정상 제출(여기에 AJAX 전송이나 백엔드 연동 코드 추가)
    alert('문의가 정상적으로 접수되었습니다! 빠른 시일 내에 답변드리겠습니다.');
    // e.preventDefault(); // 백엔드 없이 테스트 시 주석 해제
  });
</script>

</body>
</html>
