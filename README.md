# Nomeados ao Oscar

Contém a base de indicados ao Oscar em formato JSON para treinar comandos de consulta no MongoDB. 

* Quantas vezes Natalie Portman foi indicada ao Oscar?

<p>R: 3 vezes.</p>
<p>Q:</p>

```sql
SELECT COUNT(*) FROM indicados WHERE "Name" Like "%Natalie Portman%";
```

* Quantos Oscars Natalie Portman ganhou?

<p>R: 1 vez.</p>
<p>Q:</p>

```sql
SELECT COUNT(*) FROM indicados_ao_oscar WHERE nome_do_indicado LIKE	'%Natalie Portman%' AND vencedor = 'true';
```

* Amy Adams já ganhou algum Oscar?

<p>R: Não</p>
<p>Q:</p>

```sql
SELECT COUNT(*) > 0 FROM indicados_ao_oscar WHERE nome_do_indicado LIKE '%Amy Adams%' AND vencedor = 'true';
```

* A série de filmes Toy Story ganhou um Oscar em quais anos?

<p>R: 2011 e 2020</p>
<p>Q:</p>

```sql
SELECT DISTINCT ano_cerimonia FROM indicados_ao_oscar WHERE vencedor = 'true' AND nome_do_filme LIKE '%Toy Story%';
```

* A partir de que ano que a categoria "Actress" deixa de existir? 

<p>R: A partir de 1976</p>
<p>Q:</p>

```sql
SELECT ano_cerimonia FROM indicados_ao_oscar WHERE categoria = 'Actress' ORDER BY ano_cerimonia DESC LIMIT 1;
```

* Quem ganhou o primeiro Oscar para Melhor Atriz? Em que ano?

<p>R: Marie-Christine Barrault, em 1977</p>
<p>Q:</p>

```sql
SELECT nome_do_indicado, ano_cerimonia FROM indicados_ao_oscar 
WHERE categoria = 'ACTRESS IN A LEADING ROLE' 
ORDER BY ano_cerimonia LIMIT 1;
```

* Na campo "Vencedor", altere todos os valores com "true" para 1 e todos os valores "false" para 0.

<p>Q:</p>

```sql
UPDATE indicados_ao_oscar SET vencedor = 1 WHERE vencedor = 'true';
UPDATE indicados_ao_oscar SET vencedor = 0 WHERE vencedor = 'false';
```

* Em qual edição do Oscar "Crash" concorreu ao Oscar?

<p>R: Em 2006</p>
<p>Q:</p>

```sql
SELECT ano_cerimonia FROM indicados_ao_oscar WHERE nome_do_filme = 'Crash' LIMIT 1;
```

* O filme Central do Brasil aparece no Oscar?

<p>R: Sim</p>
<p>Q:</p>

```sql
SELECT COUNT(*) > 0 FROM indicados_ao_oscar WHERE nome_do_filme LIKE '%Central Station%';
```

* Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser.

<p>R: Sim</p>
<p>Q:</p>

```sql
INSERT INTO indicados_ao_oscar (ano_filmagem, ano_cerimonia, cerimonia, categoria, nome_do_indicado, nome_do_filme, vencedor)
VALUES (2024, 2025, 97, 'ACTRESS IN A LEADING ROLE', 'Demi Moore', 'The Substance', 1), 
(2024, 2025, 97, 'ACTRESS IN A LEADING ROLE', 'Blake Lively', 'É assim que acaba', 0),
(2023, 2024, 96, 'ACTRESS IN A LEADING ROLE', 'Kiernan Shipka', 'Dezesseis Facadas', 1);
```

* Denzel Washington já ganhou algum Oscar?

<p>R: Não</p>
<p>Q:</p>

```sql
SELECT COUNT(*) > 0 FROM indicados_ao_oscar WHERE nome_do_indicado LIKE '%Denzel Washington%' AND vencedor LIKE 'true';
```

* Quais os filmes que ganharam o Oscar de Melhor Filme?

<p>R: Wings, The Broadway Melody, All Quiet on the Western Front, Cimarron, Grand Hotel, Cavalcade, It Happened One Night, Mutiny on the Bounty, The Great Ziegfeld, The Life of Emile Zola, You Can't Take It with You, Gone with the Wind, Rebecca, How Green Was My Valley, Mrs. Miniver, Casablanca, Going My Way, The Lost Weekend, The Best Years of Our Lives, Gentleman's Agreement, Hamlet, All the King's Men, All About Eve, An American in Paris, The Greatest Show on Earth, From Here to Eternity, On the Waterfront, Marty, Around the World in 80 Days, The Bridge on the River Kwai, Gigi, Ben-Hur, The Apartment, West Side Story, Lawrence of Arabia, Tom Jones, My Fair Lady, A Man for All Seasons, A Man and a Woman, In the Heat of the Night, Oliver!, Midnight Cowboy, Patton, The Godfather, The Godfather Part II, The Sting, One Flew Over the Cuckoo's Nest, Rocky, Annie Hall, The Deer Hunter, Kramer vs. Kramer, Ordinary People, Chariots of Fire, Gandhi, Terms of Endearment, Amadeus, Out of Africa, Platoon, The Last Emperor, Rain Man, Driving Miss Daisy, Dances with Wolves, The Silence of the Lambs, Unforgiven, Schindler's List, Forrest Gump, Braveheart, The English Patient, Titanic, Shakespeare in Love, American Beauty, Gladiator, A Beautiful Mind, The Lord of the Rings: The Return of the King, Million Dollar Baby, Crash, The Departed, No Country for Old Men, Slumdog Millionaire, The Hurt Locker, The King's Speech, The Artist, Argo, 12 Years a Slave, Birdman or (The Unexpected Virtue of Ignorance), Spotlight, Moonlight, The Shape of Water, Green Book, Parasite, Nomadland, CODA e Everything Everywhere All at Once</p>
<p>Q:</p>

```sql
SELECT DISTINCT nome_do_filme FROM indicados_ao_oscar WHERE vencedor = 1;
```

* Bonus: Quais os filmes que ganharam o Oscar de Melhor Filme e Melhor Diretor na mesma cerimonia?

<p>R: The Divine Lady, All Quiet on the Western Front, Skippy, Bad Girl, Cavalcade, It Happened One Night, The Informer, Mr. Deeds Goes to Town, The Awful Truth, You Can't Take It with You, Gone with the Wind, The Grapes of Wrath, How Green Was My Valley, Mrs. Miniver, Casablanca, Going My Way, The Lost Weekend, The Best Years of Our Lives, Gentleman's Agreement, The Treasure of the Sierra Madre, A Letter to Three Wives, All About Eve, A Place in the Sun, The Quiet Man, From Here to Eternity, On the Waterfront, Marty, Giant, The Bridge on the River Kwai, Gigi, Ben-Hur, The Apartment, West Side Story, Lawrence of Arabia, Tom Jones, My Fair Lady, The Sound of Music, A Man for All Seasons, The Graduate, In the Heat of the Night, Oliver!, Midnight Cowboy, Patton, The French Connection, Cabaret, The Godfather, The Sting, The Godfather Part II, One Flew Over the Cuckoo's Nest, Rocky, Annie Hall, The Deer Hunter, Kramer vs. Kramer, Ordinary People, Reds, Chariots of Fire, Gandhi, Terms of Endearment, Amadeus, Out of Africa, Platoon, The Last Emperor, Rain Man, Born on the Fourth of July, Driving Miss Daisy, Dances with Wolves, The Silence of the Lambs, Unforgiven, Schindler's List, Forrest Gump, Braveheart, The English Patient, Titanic, Saving Private Ryan, Shakespeare in Love, American Beauty, Traffic, Gladiator, A Beautiful Mind, The Pianist, Chicago, The Lord of the Rings: The Return of the King, Million Dollar Baby, Brokeback Mountain, Crash, The Departed, No Country for Old Men, Slumdog Millionaire, The Hurt Locker, The King's Speech, The Artist, Life of Pi, Argo, Gravity, 12 Years a Slave, Birdman or (The Unexpected Virtue of Ignorance), The Revenant, Spotlight, La La Land, Moonlight, The Shape of Water, Roma, Green Book, Parasite, Nomadland, The Power of the Dog, CODA, Everything Everywhere All at Once, e Oppenheimer</p>
<p>Q:</p>

```sql
SELECT DISTINCT nome_do_filme FROM indicados_ao_oscar WHERE categoria IN ('BEST PICTURE','DIRECTING') AND vencedor LIKE 1;
```

* Bonus: Denzel Washington e Jamie Foxx já concorreram ao Oscar no mesmo ano?

<p>R: Não</p>
<p>Q:</p>

```sql
SELECT COUNT(*) > 0
FROM indicados_ao_oscar 
WHERE nome_do_indicado IN ('Denzel Washington','Jamie Foxx') 
GROUP BY ano_cerimonia
HAVING COUNT(*) = 2;
```