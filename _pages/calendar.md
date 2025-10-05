---
layout: page
title: "学术会议日历"
# description:
permalink: /calendar/
---

<div class="calendar-container">
	<div class="conference-toggle">
		<button id="show-upcoming" class="active">即将开始的会议</button>
		<button id="show-expired">已结束的会议</button>
	</div>

    <div id="calendar"></div>

    <div class="upcoming-conferences">
        <h3>即将开始的会议</h3>
        {% assign today = "now" | date: "%Y-%m-%d" %}
        {% for conference in site.data.conferences %}
            {% if conference.status == "potential" %}
                {% comment %}
				{% assign reg_deadline = conference.registration_deadline %}
                {% endcomment %}
                {% assign reg_deadline = conference.start_date %}
                {% if reg_deadline >= today %}
                    <div class="conference-item">
                        <h4>{{ conference.title }}</h4>
                        <p>时间：{{ conference.start_date }} -- {{ conference.end_date }}</p>
                        <p>地点：{{ conference.location }}</p>
                        <p>费用：{{ conference.cost }}</p>
                        <p>注册截止日期：{{ conference.registration_deadline }}</p>
                        <p>状态：尚未注册</p>
                        <a href="{{ conference.url }}" target="_blank">立即注册</a>
                    </div>
                {% endif %}
            {% endif %}
        {% endfor %}
    </div>
    
    <div class="expired-conferences">
        <h3>已结束的会议</h3>
        {% assign today = "now" | date: "%Y-%m-%d" %}
        {% for conference in site.data.conferences %}
            {% if conference.status == "potential" %}
                {% assign end_date = conference.end_date %}
                {% if end_date < today %}
                    <div class="conference-item expired">
                        <h4>{{ conference.title }}</h4>
                        <p>时间：{{ conference.start_date }} - {{ conference.end_date }}</p>
                        <p>地点：{{ conference.location }}</p>
                    </div>
                {% endif %}
            {% endif %}
        {% endfor %}
    </div>
    
</div>

<script>
    function checkReminders() {
        const conferences = {{ site.data.conferences | jsonify }};
        const today = new Date();
        
        conferences.forEach(conference => {
            if (conference.status === "potential") {
                const regDeadline = new Date(conference.registration_deadline);
                const reminderDate = new Date(regDeadline);
                reminderDate.setDate(regDeadline.getDate() - conference.reminder_cycle);
                
                if (today >= reminderDate && today <= regDeadline) {
                    alert(`提醒：会议"${conference.title}"注册截止日期为${conference.registration_deadline}，请尽快注册！`);
                }
            }
        });
    }

    // 页面加载时检查提醒
    //window.onload = checkReminders;
	window.onload = function () {
		checkReminders();

		const upcomingBtn = document.getElementById("show-upcoming");
		const expiredBtn = document.getElementById("show-expired");
		const upcomingSection = document.querySelector(".upcoming-conferences");
		const expiredSection = document.querySelector(".expired-conferences");

		// 默认显示即将开始的会议
		upcomingSection.style.display = "block";
		expiredSection.style.display = "none";

		upcomingBtn.addEventListener("click", function () {
			upcomingSection.style.display = "block";
			expiredSection.style.display = "none";
			upcomingBtn.classList.add("active");
			expiredBtn.classList.remove("active");
		});

		expiredBtn.addEventListener("click", function () {
			upcomingSection.style.display = "none";
			expiredSection.style.display = "block";
			expiredBtn.classList.add("active");
			upcomingBtn.classList.remove("active");
		});
	};

</script>

<!-- back to top button -->
<script src="/js/vanilla-back-to-top.min.js"></script>
<script>addBackToTop()</script>

<!-- css style for switch button -->
<style>
.conference-toggle {
    margin-bottom: 20px;
}
.conference-toggle button {
    padding: 8px 16px;
    margin-right: 10px;
    cursor: pointer;
}
.conference-toggle button.active {
    background-color: #007bff;
    color: white;
    border: none;
}
</style>