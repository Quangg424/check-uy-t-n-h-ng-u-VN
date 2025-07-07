# check-uy-t-n-h-ng-u-VN
trang web giúp mọi người đánh giá uy tín
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Kiểm Tra Độ Uy Tín & Scam</title>
  <style>
    body { font-family: Arial; background: #f0f0f0; padding: 20px; }
    .container { max-width: 700px; margin: auto; background: white; padding: 30px; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    input, textarea, select, button { width: 100%; padding: 10px; margin-top: 10px; font-size: 16px; }
    .review { border-top: 1px solid #ddd; margin-top: 10px; padding-top: 10px; }
    .warning { color: red; font-weight: bold; margin-top: 10px; }
  </style>
</head>
<body>

<div class="container">
  <h2>🔍 Kiểm Tra Uy Tín Người Dùng</h2>
  <input type="text" id="username" placeholder="Nhập tên cần kiểm tra (VD: Đông, Hiếu Lê)">
  <button onclick="checkUser()">Kiểm Tra</button>

  <div id="result" style="margin-top:20px;"></div>

  <div id="reviewForm" style="display:none; margin-top:30px;">
    <h3>✍️ Gửi đánh giá</h3>
    <label>Chọn sao:</label>
    <select id="rating">
      <option value="5">5 sao - Rất uy tín</option>
      <option value="4">4 sao - Tốt</option>
      <option value="3">3 sao - Trung bình</option>
      <option value="2">2 sao - Nghi ngờ</option>
      <option value="1">1 sao - Scam!</option>
    </select>
    <textarea id="comment" placeholder="Bình luận của bạn..."></textarea>
    <button onclick="submitReview()">Gửi đánh giá</button>
  </div>
</div>

<script>
  // Danh sách người cần kiểm tra
  const users = {
    "đông": {
      name: "Đông",
      reviews: [
        { rating: 5, comment: "Giao dịch uy tín, nhiệt tình." },
        { rating: 4, comment: "Ổn, không có vấn đề gì." }
      ]
    },
    "hiếu lê": {
      name: "Hiếu Lê",
      reviews: [
        { rating: 2, comment: "Giao hàng trễ, không trả lời tin nhắn." },
        { rating: 1, comment: "Scam, mất tiền!" }
      ]
    },
    "lộc chuyên buôn": {
      name: "Lộc Chuyên Buôn",
      reviews: [
        { rating: 3, comment: "Chậm trễ, nhưng vẫn giao hàng." },
        { rating: 2, comment: "Không rõ ràng, nên cẩn trọng." }
      ]
    },
    "trần trung hiếu": {
      name: "Trần Trung Hiếu",
      reviews: [
        { rating: 5, comment: "Rất đáng tin cậy!" },
        { rating: 5, comment: "Hỗ trợ rất tốt." }
      ]
    },
    "phạm lợi": {
      name: "Phạm Lợi",
      reviews: [
        { rating: 1, comment: "Lừa đảo, đã report!" },
        { rating: 1, comment: "Không gửi hàng, chiếm đoạt tiền." }
      ]
    },
    "nam lê": {
      name: "Nam Lê",
      reviews: [
        { rating: 4, comment: "Ổn, phản hồi tốt." },
        { rating: 3, comment: "Giao trễ nhưng vẫn uy tín." }
      ]
    }
  };

  let currentUser = "";

  function checkUser() {
    const input = document.getElementById('username').value.trim().toLowerCase();
    const resultDiv = document.getElementById('result');
    const form = document.getElementById('reviewForm');

    if (!users[input]) {
      resultDiv.innerHTML = `<p>❌ Không tìm thấy người dùng <strong>${input}</strong>.</p>`;
      form.style.display = "none";
      return;
    }

    currentUser = input;
    const user = users[input];
    const reviews = user.reviews;

    let total = 0;
    let html = `<h3>🧑 Người dùng: ${user.name}</h3>`;
    reviews.forEach(r => total += r.rating);
    const avg = (total / reviews.length).toFixed(1);
    html += `<p>⭐ Điểm uy tín trung bình: <strong>${avg}</strong></p>`;

    const scamCount = reviews.filter(r => r.rating <= 2).length;
    if (scamCount >= 2) {
      html += `<p class="warning">⚠️ Cảnh báo: Có dấu hiệu lừa đảo! Nhiều đánh giá tiêu cực.</p>`;
    }

    html += `<h4>📋 Đánh giá:</h4>`;
    reviews.forEach(r => {
      html += `<div class="review">⭐ ${r.rating} – ${r.comment}</div>`;
    });

    resultDiv.innerHTML = html;
    form.style.display = "block";
  }

  function submitReview() {
    const rating = parseInt(document.getElementById('rating').value);
    const comment = document.getElementById('comment').value.trim();

    if (!comment) {
      alert("Vui lòng nhập bình luận.");
      return;
    }

    users[currentUser].reviews.push({ rating, comment });
    document.getElementById('comment').value = "";
    alert("Đánh giá đã được gửi!");
    checkUser(); // cập nhật lại thông tin
  }
</script>

</body>
</html>
