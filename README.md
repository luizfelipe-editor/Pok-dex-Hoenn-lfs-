<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8">
    <title>Pokédex de Hoenn</title>
    <style>
      body {
        font-family: Arial, "Times New Roman";
        background-color: #ff6347;
        text-align: center;
        margin: 4px;
        padding: 4px;
      }

      h1 {
        color: #f8f8ff;
        margin-top: 20px;
      }

      #pokedex {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        padding: 20px;
      }

      .pokemon-card {
        background-color: #f0f8ff;
        border: 2px solid #ddd;
        border-radius: 10px;
        width: 150px;
        margin: 10px;
        padding: 10px;
        box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
      }

      .pokemon-card img {
        width: 100px;
        padding: 10px;
      }
    </style>
  </head>
  <body>
    <h1>Pokédex - Região de Hoenn</h1>
    <div id="pokedex"></div>

    <script>
      const pokedexContainer = document.getElementById("pokedex");

      for (let i = 1; i <= 386; i++) {
        fetch(`https://pokeapi.co/api/v2/pokemon/${i}`)
          .then(response => response.json())
          .then(pokemon => {
            const card = document.createElement("div");
            card.classList.add("pokemon-card");
            card.innerHTML = `
              <h3>#${pokemon.id} - ${pokemon.name}</h3>
              <img src="${pokemon.sprites.front_default}" alt="${pokemon.name}">
              <p>Tipo: ${pokemon.types.map(t => t.type.name).join(", ")}</p>
            `;
            pokedexContainer.appendChild(card);
          })
          .catch(error => {
            console.error(`Erro ao carregar o Pokémon ${i}:`, error);
          });
      }
    </script>
  </body>
</html>
