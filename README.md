<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title>Interactive Risk Register</title>
  <script src="https://unpkg.com/sigma@2.4.0/build/sigma.min.js"></script>
  <style>
    body { margin: 0; }
    #container { width: 100vw; height: 100vh; }
  </style>
</head>
<body>
  <div id="container"></div>

  <script>
    fetch("risk_map.json")
      .then(res => res.json())
      .then(data => {
        const graph = new sigma.Graph();

        data.nodes.forEach(n => {
          graph.addNode(n.id, {
            x: n.x,
            y: n.y,
            size: n.size || 5,
            label: n.label,
            color: n.color || "#888"
          });
        });

        data.edges.forEach(e => {
          graph.addEdge(e.source, e.target);
        });

        new sigma.Sigma(graph, document.getElementById("container"));
      });
  </script>
</body>
