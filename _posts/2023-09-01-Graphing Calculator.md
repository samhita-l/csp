---
toc: true
comments: false
layout: post
title: Graphing Calculator
description: Love Math
type: hacks
courses: { csp: {week: 1} }

---

<html>
<head>
    <title>Advanced Graphing Calculator</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/11.9.0/math.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        #calculator {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 80px;
        }
        canvas {
            max-width: 600px;
        }
    </style>
</head>
<body>
    <div id="calculator">
        <h1>Advanced Graphing Calculator</h1>
        <input type="text" id="expression" placeholder="Enter an expression (e.g., sin(x), x^2)">
        <button onclick="graph()">Graph</button>
        <button onclick="calculateDerivative()">Calculate Derivative</button>
        <button onclick="calculateIntegral()">Calculate Integral</button>
        <canvas id="graphCanvas"></canvas>
    </div>


    <script>
        const expressionInput = document.getElementById("expression");
        const graphCanvas = document.getElementById("graphCanvas");
        const parser = math.parser();


        function graph() {
            const expression = expressionInput.value;


            // Create x values for the graph
            const xValues = math.range(-10, 10, 0.1).toArray();


            // Evaluate the expression for each x value
            const yValues = xValues.map(x => parser.evaluate(expression, { x }));


            // Prepare data for Chart.js
            const data = {
                labels: xValues,
                datasets: [{
                    label: expression,
                    data: yValues,
                    fill: false,
                    borderColor: 'blue',
                    borderWidth: 2,
                }]
            };


            // Create a line chart using Chart.js
            new Chart(graphCanvas, {
                type: 'line',
                data: data,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: {
                            type: 'linear',
                            position: 'bottom'
                        },
                        y: {
                            type: 'linear',
                            position: 'left'
                        }
                    }
                }
            });
        }


        function calculateDerivative() {
            const expression = expressionInput.value;
            const derivative = math.derivative(expression, 'x').toString();
            alert(`Derivative: ${derivative}`);
        }


        function calculateIntegral() {
            const expression = expressionInput.value;
            const integral = math.integral(expression, 'x').toString();
            alert(`Integral: ${integral}`);
        }
    </script>
</body>
</html>

 






