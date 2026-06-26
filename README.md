```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>AI Workout Coach</title>
    <!-- PWA Meta Tags -->
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black">
    <meta name="apple-mobile-web-app-title" content="AI Coach">
    <style>
        :root { --primary: #007AFF; --bg: #f2f2f7; --card: #ffffff; }
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background: var(--bg); padding: 20px; margin: 0; }
        .container { max-width: 500px; margin: 0 auto; }
        .card { background: var(--card); padding: 20px; border-radius: 16px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); margin-bottom: 20px; }
        h1 { font-size: 24px; color: #1c1c1e; }
        label { display: block; margin: 10px 0 5px; font-weight: 600; }
        select, input, button { width: 100%; padding: 12px; border-radius: 10px; border: 1px solid #ccc; font-size: 16px; margin-bottom: 10px; box-sizing: border-box; }
        button { background: var(--primary); color: white; border: none; font-weight: bold; cursor: pointer; }
        #output { white-space: pre-wrap; line-height: 1.5; font-size: 15px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>AI Workout Coach</h1>
        <div class="card">
            <label>Environment</label>
            <select id="env"><option>Gym</option><option>Home</option></select>
            <label>Focus</label>
            <input type="text" id="focus" placeholder="e.g., Legs, Chest/Triceps">
            <button onclick="generateWorkout()">Generate Workout</button>
        </div>
        <div class="card">
            <div id="output">Workout will appear here...</div>
        </div>
    </div>

    <script>
        const API_KEY = "AQ.Ab8RN6ItjcHNJ_IzJ7MDPRZLhSgFqQuwVNuWpX74Kc1ixFkHPw";
        async function generateWorkout() {
            const env = document.getElementById('env').value;
            const focus = document.getElementById('focus').value;
            const output = document.getElementById('output');
            
            output.innerText = "Consulting the AI...";
            
            const prompt = `You are a scientific strength coach. Create a ${env} workout targeting ${focus}. 
            Include: 
            1. List of exercises (sets/reps).
            2. 'Scientific Rationale' for muscle group selection and recovery.
            Format clearly for a mobile screen.`;

            try {
                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${API_KEY}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ contents: [{ parts: [{ text: prompt }] }] })
                });
                const data = await response.json();
                output.innerText = data.candidates[0].content.parts[0].text;
            } catch (err) {
                output.innerText = "Error: Ensure your API Key is set correctly.";
            }
        }
    </script>
</body>
</html>

```
