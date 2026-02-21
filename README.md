      var box1 = document.getElementById('box1')
        var box2 = document.getElementById('box2')
        var box3 = document.getElementById('box3')
        var inside1 = document.getElementById("inside1")
        var inside2 = document.getElementById("inside2")
        var inside3 = document.getElementById("inside3")
        var vie = document.getElementById("vie")
        var retry = document.getElementById("retry")
        var box1Top = 0
        var box2Top = 0
        var box3Top = 0
        var essaiUser = 0
        var deplacement = 2
        var score = document.getElementById("score");
        var points = 0
        var box1Left = 400
        var box2Left = 800
        var box3Left = 1200
        var speed = 1
        var reponse = document.getElementById('reponse')
        var lives = 900
        var box1Stats = 0.8 + Math.random() * 0.3; 
        var box2Stats = 0.5 + Math.random() * 0.3;
        var box3Stats = 0.3 + Math.random() * 0.3;  


        var slow = null
        if (points < 100) {
            array = ['your', 'you', 'year', 'would','work','with','will','who','which','when','well','we','way','want','use','us','two','to','time','this','think','they','these','there','then','them','their','the','that','than','take','some','so','she','see','say','people','over','out','our','other','or','only','one','on','now','not','no','new','my','most','me','make','look','like','know','just','its','it','into','in','if','I','how','him','her','he','have','good','go','give','get','from','for','first','even']
        } else if (points < 300) {
            array = ['because', 'through', 'thought', 'believe', 'country', 'example', 'problem', 'develop', 'between', 'system','company', 'control', 'perhaps', 'several', 'whether', 'support', 'hundred', 'happen', 'change', 'before', 'always', 'course', 'market', 'energy', 'effect', 'public', 'reason', 'result', 'second', 'simple']
        } else if (points < 500) {
            array = ['questionnaire', 'unnecessary', 'consciousness', 'environment', 'opportunity', 'government', 'successful', 'immediately', 'beautiful', 'experience', 'individual', 'necessary', 'commission', 'committee', 'understand', 'particular', 'therefore', 'knowledge', 'development', 'character', 'different', 'attention', 'information', 'discussion']
        } else {
            array = ['pneumonoultramicroscopicsilicovolcanoconiosis', 'antidisestablishmentarianism', 'supercalifragilisticexpialidocious', 'pseudopseudohypoparathyroidism', 'floccinaucinihilipilification', 'uncharacteristically', 'electroencephalograph',  'photographically', 'straightforwardly', 'uncompromisingly', 'incomprehensibility', 'honorificabilitudinitatibus', 'lymphangioleiomyomatosis', 'sesquipedalianism', 'counterproductiveness']
        }

        var boxCounter1 = Math.floor(Math.random() * array.length);
        var boxCounter2 = Math.floor(Math.random() * array.length);
        var boxCounter3 = Math.floor(Math.random() * array.length);


        for(i=0; i<array.length;i++) {
            console.log(array[i])
        }
        
        function specialBox() {
            box1.style.boxShadow = ""
            box1.style.boxShadow = ""
            box1.style.boxShadow = ""
            life = Math.random() > 0.95
            console.log(life)
            if (life) {
                box1.style.boxShadow = "0 0 40px 10px rgba(230, 79, 24, 0.7)";
            }
            else {
                slow = Math.random() > 0.99;
                if (slow) {
                    box1.style.boxShadow = '0 0 40px 10px rgba(75, 0, 192, 0.7)';
                } else {
                    box1.style.boxShadow = ""
                }
            }
        }
        function updateBox(){
            inside1.innerHTML = array[boxCounter1]
            inside2.innerHTML = array[boxCounter2]
            inside3.innerHTML = array[boxCounter3]
        }
        function dropBox() {
            box1Top += speed * 2 * box1Stats
            box2Top += speed * 2 * box2Stats
            box3Top += speed * 2 * box3Stats
            box1.style.top = box1Top + 'px'
            box2.style.top = box2Top + 'px'
            box3.style.top = box3Top + 'px'

            box1Left += deplacement
            box2Left -= deplacement
            box3Left += deplacement
            box1.style.left = box1Left + 'px'
            box2.style.left = box2Left + 'px'
            box3.style.left = box3Left + 'px'
            
            if(box1Left > 600 || box1Left < 200) {
                deplacement = -deplacement;
            }

            if(box2Left > 600 || box2Left < 1000) {
                deplacement = -deplacement;
            }
            
            if(box3Left > 1000 || box3Left < 1400) {
                deplacement = -deplacement;
            }

            if (box1Top > 1000) {
                box1Top = 0
                boxCounter1 += 3
                lives -= 180;
                vie.style.left = "calc(80% - " + (lives / 2) + "px)";
                vie.style.width = lives + "px";
                specialBox()
            }

            if (box2Top > 1000) {
                box2Top = 0
                boxCounter2 += 3
                lives -= 180;
                vie.style.left = "calc(80% - " + (lives / 2) + "px)";
                vie.style.width = lives + "px";
                specialBox()
            }

            if (box3Top > 1000) {
                box3Top = 0
                boxCounter3 += 3
                lives -= 180;
                vie.style.left = "calc(80% - " + (lives / 2) + "px)";
                vie.style.width = lives + "px";
                specialBox()
            }

            if (lives <= 0) {
                retry.style.opacity = 1;
                retry.style.pointerEvents = 'auto';
                box1.style.opacity = 0;
                box2.style.opacity = 0;
                box3.style.opacity = 0;
            }
            updateBox()
        }

        setInterval(dropBox, 10)
        updateBox()
        document.addEventListener('keydown', clavier)
        console.log(array.length)
        
        function clavier(e) {
            if(e.keyCode === 13) {
                essaiUser = document.getElementById('reponse').value
                console.log(essaiUser)
                document.getElementById('reponse').value = ''
            }
            if(essaiUser === array[boxCounter1]) {
                points += array[boxCounter1].length
                boxCounter1 = Math.floor(Math.random() * array.length);
                box1Top = 0
                specialBox()
                speed += 0.1
                if (life) {
                    lives += 180
                    vie.style.left = "calc(80% - " + (lives / 2) + "px)";
                    vie.style.width = lives + "px";
                    life = false
                }
                if (slow) {
                    speed = 1
                    slow = false
                }
                score.innerHTML = "Score : " + points
                if(boxCounter >= array.length) {
                    boxCounter = 0
                }
            } else if (essaiUser === array[(boxCounter2)]) {
                points += array[boxCounter2].length
                boxCounter2 = Math.floor(Math.random() * array.length);
                box2Top = 0
                specialBox()
                speed += 0.1
                if (life) {
                    lives += 180
                    vie.style.left = "calc(80% - " + (lives / 2) + "px)";
                    vie.style.width = lives + "px";
                    life = false
                }
                if (slow) {
                    speed = 1
                    slow = false
                }
                score.innerHTML = "Score : " + points
                if(boxCounter >= array.length) {
                    boxCounter = 0
                }
            } else if (essaiUser === array[(boxCounter3)]) {
                boxCounter3 = Math.floor(Math.random() * array.length);
                points += array[boxCounter3].length
                box3Top = 0
                specialBox()
                speed += 0.1
                if (life) {
                    lives += 180
                    vie.style.left = "calc(80% - " + (lives / 2) + "px)";
                    vie.style.width = lives + "px";
                    life = false
                }
                if (slow) {
                    speed = 1
                    slow = false
                }
                score.innerHTML = "Score : " + points
                if(boxCounter >= array.length) {
                    boxCounter = 0
                }
            }
        }
