<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>דף נחיתה מקצועי</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
    <style>
        body {
            /* רקע תכלת בהיר לדף הכללי */
            background-color: #e0f2fe; 
            font-family: system-ui, -apple-system, sans-serif;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }
        
        .container-shadow {
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }

        /* מכל המודעה עם הסתרת שולי הדרייב */
        .ad-container-outer {
            position: relative;
            width: 100%;
            padding-top: 141.4%; /* יחס A4 */
            overflow: hidden;
            border-radius: 1rem;
            transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            background: white;
        }

        .ad-container-outer:hover {
            transform: scale(1.02);
        }

        .ad-container-outer iframe {
            position: absolute;
            top: -50px; 
            left: 0;
            width: 100%;
            height: calc(100% + 100px); 
            border: none;
            pointer-events: none;
        }

        /* הגדרות דף הסליקה - ללא חיתוך, עם רקע לבן */
        .payment-section {
            position: relative;
            background: #ffffff !important;
            border-radius: 1.5rem;
            overflow: hidden;
            z-index: 1;
        }

        .payment-iframe-wrapper {
            background: #ffffff !important;
            width: 100%;
            display: flex;
            justify-content: center;
        }

        .payment-iframe {
            width: 100%;
            /* גובה סטטי גבוה למניעת גלילה פנימית */
            height: 2500px; 
            border: none;
            display: block;
            overflow: hidden;
            background: #ffffff !important;
        }

        @media (max-width: 640px) {
            .payment-iframe {
                height: 3200px; 
            }
        }

        /* אפקט חשיפה עדין */
        .reveal {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease-out;
        }
        
        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }
    </style>
</head>
<body class="py-10 px-4 md:py-16">
    <div class="max-w-4xl mx-auto space-y-12">
        
        <!-- Ad Section - Frameless Look -->
        <section class="reveal bg-white rounded-2xl container-shadow ad-container-outer animate__animated animate__fadeIn">
            <iframe 
                src="https://drive.google.com/file/d/1Va8OrgSTUu1g74O1ACiu6RoWmhZEqBGv/preview" 
                allow="autoplay">
            </iframe>
        </section>

        <!-- Animated Divider -->
        <div class="flex items-center justify-center space-x-4 space-x-reverse opacity-40">
            <div class="h-px bg-sky-500 flex-grow"></div>
            <div class="w-2 h-2 bg-sky-600 rounded-full animate-ping"></div>
            <div class="h-px bg-sky-500 flex-grow"></div>
        </div>

        <!-- Payment Section -->
        <section class="reveal payment-section container-shadow animate__animated animate__fadeInUp">
            <div class="payment-iframe-wrapper">
                <iframe 
                    src="https://secure.cardcom.solutions/EA/EA5/BbTLfzr4MkuwlnDPAanA8g/PaymentSP" 
                    class="payment-iframe"
                    id="paymentFrame"
                    scrolling="no"
                    frameborder="0"
                    loading="lazy">
                </iframe>
            </div>
        </section>

        <!-- Footer with the requested text -->
        <footer class="py-12 text-center">
            <h2 class="text-xl md:text-2xl font-bold text-sky-900 animate__animated animate__pulse animate__infinite italic">
                יחי אדוננו מורנו ורבינו מלך המשיח לעולם ועד
            </h2>
        </footer>
    </div>

    <script>
        // פונקציית חשיפה בגלילה
        function reveal() {
            var reveals = document.querySelectorAll(".reveal");
            for (var i = 0; i < reveals.length; i++) {
                var windowHeight = window.innerHeight;
                var elementTop = reveals[i].getBoundingClientRect().top;
                var elementVisible = 100;
                if (elementTop < windowHeight - elementVisible) {
                    reveals[i].classList.add("active");
                }
            }
        }

        window.addEventListener("scroll", reveal);
        window.onload = function() {
            reveal();
            const frame = document.getElementById('paymentFrame');
            if(frame) {
                frame.style.height = window.innerWidth < 640 ? "3200px" : "2500px";
            }
        };

        // האזנה להודעות גובה
        window.addEventListener('message', function(e) {
            if (e.data && e.data.height) {
                const frame = document.getElementById('paymentFrame');
                frame.style.height = (e.data.height + 50) + 'px';
            }
        }, false);
    </script>
</body>
</html>
