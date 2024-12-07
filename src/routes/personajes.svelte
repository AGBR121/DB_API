<script>
    export let name;
    export let ki;
    export let maxKi;
    export let race;
    export let image;
  </script>
  
  <div class="character-card">
    <img src={image} alt={name} class="character-image" />
    <h2>{name}</h2>
    <p><strong>Ki:</strong> {ki}</p>
    <p><strong>Max Ki:</strong> {maxKi}</p>
    <p><strong>Race:</strong> {race}</p>
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
  
    .character-image {
    width: 100%;
    height: auto;
    max-height: 200px;
    object-fit: contain;
    border-radius: 8px;
    margin-bottom: 10px;
}
  
    .character-card h2 {
      color: orangered;
      margin-bottom: 10px;
    }
  
    .character-card p {
      margin: 5px 0;
    }
  </style>
  