// ฟังก์ชันสร้างปุ่ม Google Calendar
function showBookingSummaryFromForm() {
  const carName = document.querySelector("#summary .car-name")?.textContent || "รถเช่า";
  const startDate = document.getElementById("startDate").value;
  const endDate = document.getElementById("endDate").value;
  const startTime = document.getElementById("pickupTime").value;
  const pickup = document.getElementById("pickupLocation").value;
  const returnLoc = document.getElementById("returnLocation").value;

  const summaryEl = document.getElementById("summary");
  const calendarBtn = document.createElement("button");
  calendarBtn.textContent = "➕ เพิ่มลง Google Calendar";
  calendarBtn.className = "btn-ghost";
  calendarBtn.style.marginTop = "10px";

  calendarBtn.addEventListener("click", () => {
    const start = startDate.replace(/-/g, "") + "T" + startTime.replace(":", "") + "00Z";
    const end = endDate.replace(/-/g, "") + "T" + startTime.replace(":", "") + "00Z";
    const title = encodeURIComponent(`จองรถเช่า ${carName} | CarGo`);
    const details = encodeURIComponent(`รับรถ: ${pickup}\nคืนรถ: ${returnLoc}`);
    const location = encodeURIComponent(pickup);

    const gcalUrl = `https://calendar.google.com/calendar/r/eventedit?text=${title}&dates=${start}/${end}&details=${details}&location=${location}`;
    window.open(gcalUrl, "_blank");
  });

  // ใส่ปุ่มไว้ท้ายสรุปการจอง
  summaryEl.appendChild(calendarBtn);
}

// ฟัง event ตอน submit ฟอร์ม
document.getElementById("checkoutForm").addEventListener("submit", function(e) {
  e.preventDefault(); // ป้องกันรีเฟรช
  // โค้ดเดิมที่บันทึกข้อมูลการจอง...
  
  // แสดงปุ่ม Google Calendar
  showBookingSummaryFromForm();
});
