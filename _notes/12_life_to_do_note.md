<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>Cony ETF 배당금 비교표</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    table { border-collapse: collapse; width: 100%; margin-top: 20px; }
    th, td { border: 1px solid #ccc; padding: 8px; text-align: center; }
    th { background-color: #f4f4f4; }
    input[type="number"] { width: 100px; }
    .input-row { margin-bottom: 10px; }
  </style>
</head>
<body>

  <h1>Cony ETF 투자금 대비 배당금 비교</h1>

  <form id="data-form">
    <div class="input-row">
      <label>월 (예: 2025-08): <input type="month" id="month" required></label>
    </div>
    <div class="input-row">
      <label>투자금액 (₩): <input type="number" id="invest" required></label>
    </div>
    <div class="input-row">
      <label>배당금액 (₩): <input type="number" id="dividend" required></label>
    </div>
    <button type="submit">추가</button>
  </form>

  <table id="result-table">
    <thead>
      <tr>
        <th>월</th>
        <th>투자금액 (₩)</th>
        <th>배당금액 (₩)</th>
        <th>수익률 (%)</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <script>
    const form = document.getElementById('data-form');
    const tableBody = document.querySelector('#result-table tbody');

    const data = [];

    form.addEventListener('submit', function (e) {
      e.preventDefault();

      const month = document.getElementById('month').value;
      const invest = parseFloat(document.getElementById('invest').value);
      const dividend = parseFloat(document.getElementById('dividend').value);

      const roi = ((dividend / invest) * 100).toFixed(2);

      data.push({ month, invest, dividend, roi });

      updateTable();
      form.reset();
    });

    function updateTable() {
      tableBody.innerHTML = '';
      data.forEach(row => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${row.month}</td>
          <td>${row.invest.toLocaleString()}</td>
          <td>${row.dividend.toLocaleString()}</td>
          <td>${row.roi}</td>
        `;
        tableBody.appendChild(tr);
      });
    }
  </script>
</body>
</html>
