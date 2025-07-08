erDiagram
    
    GoalType {
        PERCENTAGE
        AMOUNT
    }

    EntryType {
        BUY
        SELL
    }

    USER {
        Long id
        String name
        String email
        String phone
    }

    PORTFOLIO {
        Long id
        String name
        Long userId
    }
    USER ||--o{ PORTFOLIO : owns

    ASSET {
        Long id
        String ticker
        String name
        String type
    }
    ASSET ||--o{ PORTFOLIO_ASSET : represented_by
    ASSET ||--o{ ASSET_PRICE : has

    PORTFOLIO_ASSET {
        Long id
        Long portfolioId
        Long assetId
        BigDecimal quantity
    }
    PORTFOLIO ||--|{ PORTFOLIO_ASSET : contains

    ASSET_PRICE {
        Long id
        String ticker
        LocalDateTime date
        BigDecimal price
    }

    ENTRY {
        Long id
        Long portfolioId
        Long assetId
        EntryType type
        LocalDateTime date
        BigInteger amount
    }
    PORTFOLIO ||--|{ ENTRY : records
    ENTRY ||--|| ASSET : targets
    ENTRY ||--|| EntryType : targets

    GOAL {
        Long id
        Long portfolioId
        Long assetId
        GoalType type
        BigDecimal percentage
        BigInteger amount
    }
    PORTFOLIO ||--|{ GOAL : contains
    GOAL ||--|| ASSET : targets
    GOAL ||--|| GoalType : targets
