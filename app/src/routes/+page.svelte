<script>
    let input = '';
    let lix = 0;
    let punctAmount;
    let wordList;
    let wordAmount;
    let longWordAmount;

    function calculateLix(tekst)
    {
        if(tekst.length >= 1)
           punctAmount = 0;
           for(var i = 0; i < tekst.length; i++)
           {
               if(tekst[i] == '.')
               {
                   punctAmount += 1;
               }
           }
           if (punctAmount < 1) 
           {
                punctAmount = 1
           }
           wordList = tekst.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()]/g, '').split(' ');
           wordAmount = wordList.length;
           longWordAmount = 0;
           for(var i = 0; i < wordList.length; i++)
           {
               if(wordList[i].length >= 7)
               {
                   longWordAmount += 1;
               }
           }
           lix = Math.round((wordAmount / punctAmount) + (longWordAmount * 100 / wordAmount));
    };
</script>

<head>
    <style lang="scss">@import "../styles/app.scss";</style>
    <title>LixRegner</title>
</head>

<body>
    <h1>LixRegner</h1>
    
    <input placeholder="Tekst her!" on:input={()=>calculateLix(input)} bind:value={input}>
    
    <div>
        <pre>Tekstens lixtal er {lix}</pre>
    </div>

    <div>
        <pre>
        (55+) Meget svær, faglitteratur på akademisk niveau, lovtekster.
        (45-54) Svær, f.eks. saglige bøger, populærvidenskabelige værker, akademiske udgivelser.
        (35-44) Middel, f.eks. dagblade og tidsskrifter.
        (25-34) Let for øvede læsere, f.eks. ugebladslitteratur og skønlitteratur for voksne.
        (24-) Let tekst for alle nylæsere, f.eks. børnelitteratur.
        </pre>
    </div>
</body>