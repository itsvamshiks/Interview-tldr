

## Card Deck System Design

### Entities Involved 
 - Card - belongs to one of 4 suites, with a value
 - Deck - Consists of 52 cards, 13 cards of each suite
 - Hand - Basically the player involved in the game, and the cards he has

```
public enum Suit{
    SPADE,
    HEART,
    CLUB,
    DIAMOND
}

public abstract class Card{
    private SUIT suit;
    private int value;
    private boolean isAvailable;
    
    public Card(SUIT suit,int value){
        this.suit = suit; 
        this.value = value;
        this.isAvailable = true;
    }
    
    public abstract int getValue();
    
    public void setIsAvailable(boolean isAvailable){
        this.isAvailable = isAvailable;
    }
    
}

public class BlackJackCard extends Card{


    public BlackJackCard(SUIT suit,int value){
        super(suit,value);
    }
    
    public int getValue(){
    
        if(isAce(this.value))
            return 1;
        else if(isFaceCard(this.value))
            return 10;
        else
            return this.value;
            
        
    }
    
    public boolean isAce(int value){
        return value == '1';
    }
    
    public boolean isFaceCard(int value){
        return 10 < value  && value <= 13;
    }

}

public class Deck {

    private List<Card> cardDeck;
    
    public Deck(){
        this.cardDeck = new ArrayList<BlackJackCard>();
        for(int value = 1; value <=13;value++){
            for(SUIT suite : SUIT.values()){
                cardDeck.add(new BlackJackCard(suite,value));
            }
        }
        
    }
    
    public void shuffle(){
        Random rand = new Random();
        
        for(int i = 0;i<20;i++){
            int firstCard = rand.nextInt(52);
            int secondCard = rand.nextInt(52);
            Collections.swap(cardDeck,firstCard,secondCard);
        }
    }
    
    public Card dealCard(){
        Random rand = new Random();
        int cardIndex = rand.nextInt(52);
        while(!this.cardDeck.get(cardIndex).isAvailable)
            cardIndex++;
            
        BlackJackCard card =  this.cardDeck.get(cardIndex);
        card.setIsAvailable(false);
        return this.cardDeck.get(card);
        
    }
    
    public int getCardCount(){
        return this.cardDeck.size();
    }
    
}

public Hand{
    private List<BlackJackCard> playerCards;
    
    public Hand(){
        this.playerCards = new ArrayList<BlackJackCard>();
    }
    
    public List<BlackJackCard> getHand(){
        return this.playerCards;
    }
    
    public int getScore(){
        int score = 0;
        
        for(BlackJackCard card : playerCards){
            score += card.getValue();
        }
    }

}

```
