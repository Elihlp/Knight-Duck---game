# 🦆 Knight Duck (Cavaleiro-Pato)

Um jogo **retrô, arcade e de ação**, onde você controla um bravo cavaleiro-pato em batalhas contra inimigos bizarros!  
📌 Lançamento previsto: **Setembro ~ Outubro 2025**  
📌 Plataforma de lançamento: [Itch.io](https://elihlp.itch.io/)

---

## 🎮 Controles do Jogador
- **Mover:** `A` e `D`
- **Pular:** `W` ou `ESPAÇO`
- **Usar Poção:** `E`

---

## 👾 Inimigos
- **Passáro** → voa para a esquerda; se colidir com o player, cai.  
- **Canhão** → dispara projéteis a cada 2–3 segundos.  
- **Caveira** → ao detectar o player, espera 2s e explode.  

---

## 🖥️ HUD
- **Vidas**  
- **Poções**  

---

## 👥 Público-Alvo
- Quem gosta de **plataformas retrô**, estilo **arcade/ação**.  

---

## 🚀 Roadmap de Desenvolvimento
- [x] Definição de mecânicas básicas  
- [ ] Protótipo jogável  
- [x] Implementar Passáro inimigo  
- [x] Implementar Canhão inimigo  
- [ ] Implementar Caveira inimiga  
- [x] HUD funcional (vidas e poções)
- [ ] Sistema de Level
- [ ] Sistema de Aprimoramento
- [ ] Publicar demo no Itch.io  
- [ ] Lançamento final  

---

## 📢 Acompanhe
- Itch.io: [https://elihlp.itch.io/](https://elihlp.itch.io/)  

---

## Devlogs
Todos os códigos são em Linguagem GML

- **Devlog 1**
- Comecei fazendo as sprites do player e inimigos. Depois entrei no GameMaker criei um Projeto. Dentro deste projeto eu importei a sprites do player e criei um objeto do player para PROGAMAR as mecanicas do player
- Fazendo a MOVIMENTAÇÃO do player. Código :
- 
**CREATE**
  
**Variaveis de movimento**

hspd            = 0;

hspd_max        = 2;

vspd            = 0;

vspd_max        = 5;

grav            = .3;

**Variaveis de input**

right            = false;

left             = false;

jump             = false;

shot             = false;


**Variavel de tempo para poder atirar**

timer_shot = 0;


**Método para pegar os inputs**

inputs = function(){

    right        = keyboard_check(ord("D")) or keyboard_check(vk_right);
    
    left         = keyboard_check(ord("A")) or keyboard_check(vk_left);
    
    jump         = keyboard_check_pressed(vk_space) or keyboard_check_pressed(ord("W"));
    
    shot         = keyboard_check(ord("V"));
}


**Método de movimento**

movimento = function(){

    hspd = (right - left) * hspd_max;

    
    move_and_collide(hspd, 0, colisores, 4);
    
    move_and_collide(0, vspd, colisores, 34);
}


**Método para pular**

pular = function(){

    var chao = place_meeting(x, y+1, colisores);
    
    if(!chao){
    
        vspd += grav;
        
    }
    if(chao){
    
        vspd = 0;
        
        if(jump){
        
            vspd -= vspd_max;
            
        } 
    }
}


**Método para atirar**

atirar = function(spd_shot = 1){

    timer_shot--;
    
    if(timer_shot <= 0){
    
        if(shot){
        
            var fire = instance_create_layer(x, y, "tiros", obj_tiro_player);
            
            if(xscale == 1){
            
                fire.hspeed = spd_shot;
                
                fire.image_angle = fire.direction;
                
            }
            
            else if(xscale == -1){
            
                fire.hspeed = -spd_shot;
                
                fire.image_angle = fire.direction;
                
            }
            
            timer_shot = 20;
            
        }  
    }
}


**STEP**

inputs();

movimento();

pular();

atirar(6);
