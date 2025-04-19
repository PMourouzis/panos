# panos
pasxa
<!DOCTYPE html>
<html lang="el">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Υπολογισμός Πάσχα</title>
</head>
<body>
    <h2>Υπολογισμός ημερομηνίας Πάσχα</h2>
    <label for="yearInput">Εισάγετε ένα έτος:</label>
    <input type="number" id="yearInput">
    <button onclick="calculateEaster()">Υπολογισμός</button>
    <p id="result"></p>

    <script>
        function calculateEaster() {
            let year = document.getElementById("yearInput").value;
            if (year < 1583) {
                document.getElementById("result").innerText = "Το έτος πρέπει να είναι μεγαλύτερο ή ίσο με 1583.";
                return;
            }

            // Υπολογισμός Καθολικού Πάσχα (Γρηγοριανό ημερολόγιο)
            let a = year % 19;
            let b = Math.floor(year / 100);
            let c = year % 100;
            let d = Math.floor(b / 4);
            let e = b % 4;
            let f = Math.floor((b + 8) / 25);
            let g = Math.floor((b - f + 1) / 3);
            let h = (19 * a + b - d - g + 15) % 30;
            let i = Math.floor(c / 4);
            let k = c % 4;
            let l = (32 + 2 * e + 2 * i - h - k) % 7;
            let m = Math.floor((a + 11 * h + 22 * l) / 451);
            let monthCatholic = Math.floor((h + l - 7 * m + 114) / 31);
            let dayCatholic = ((h + l - 7 * m + 114) % 31) + 1;

            // Υπολογισμός Ορθόδοξου Πάσχα (Ιουλιανό ημερολόγιο)
            let x = (year % 4);
            let y = (year % 7);
            let z = (year % 19);
            let orthodoxH = (19 * z + 15) % 30;
            let orthodoxI = (2 * x + 4 * y + 6 * orthodoxH + 6) % 7;
            let orthodoxJ = orthodoxH + orthodoxI;
            let dayOrthodox = 4 + orthodoxJ;
            let monthOrthodox = (dayOrthodox > 30) ? 5 : 4;
            dayOrthodox = (dayOrthodox > 30) ? (dayOrthodox - 30) : dayOrthodox;

            document.getElementById("result").innerText =`Το Ορθόδοξο Πάσχα το ${year} εορτάζεται στις ${dayOrthodox}/${monthOrthodox}.\n`+
                `Το Καθολικό Πάσχα το ${year} εορτάζεται στις ${dayCatholic}/${monthCatholic}.\n`
                ;
        }
    </script>
</body>
</html>
