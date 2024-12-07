<script>
    export let name;
    export let ki;
    export let maxKi;
    export let race;
  </script>
  
  <div class="character-card">
    <h2>{name}</h2>
    <p><strong>Ki:</strong> {ki}</p>
    <p><strong>Max Ki:</strong> {maxKi}</p>
    <p><strong>Raza:</strong> {race}</p>
  </div>
  
  <style>
    .character-card {
      border: 1px solid #ccc;
      border-radius: 8px;
      padding: 10px;
      margin: 10px;
      background-color: #f9f9f9;
      max-width: 300px;
      text-align: center;
      box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    }
    .character-card h2 {
      color: orangered;
      margin-bottom: 10px;
    }
    .character-card p {
      margin: 5px 0;
    }
  </style>
  