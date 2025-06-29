graph TD
    A[Start] --> B[Initialize WordPredictor];
    B --> C[Load Predefined Word Embeddings];
    C --> D[Main Loop / User Interaction];

    D -- "User chooses 'Predict Similar Word'" --> E[Input: Target Word];
    E --> F{Is Target Word in Vocabulary?};
    F -- No --> G["Output: 'Word not found'"];
    F -- Yes --> H[Get Target Word's Vector];
    H --> I[Initialize max_similarity = -1.0, most_similar_word = ""];
    I --> J[For each Word in Vocabulary (excluding Target Word)];
    J --> K[Calculate Cosine Similarity between Target Vector and Current Word's Vector];
    K --> L{Is Current Similarity > max_similarity?};
    L -- Yes --> M[Update max_similarity, most_similar_word];
    L -- No --> J; // Continue loop
    M --> J; // Continue loop (after update)
    J -- End Loop --> N[Output: Most Similar Word and Similarity Score];
    N --> D; // Back to main loop or End

    D -- "User chooses 'Solve Analogy (A - B + C)'" --> O[Input: Words A, B, C];
    O --> P{Are A, B, C all in Vocabulary?};
    P -- No --> Q["Output: 'One or more words not found'"];
    P -- Yes --> R[Get Vectors for A, B, C];
    R --> S[Calculate Resulting Vector: Vector(A) - Vector(B) + Vector(C)];
    S --> T[Initialize max_similarity = -1.0, best_match_word = ""];
    T --> U[For each Word in Vocabulary (excluding A, B, C)];
    U --> V[Calculate Cosine Similarity between Resulting Vector and Current Word's Vector];
    V --> W{Is Current Similarity > max_similarity?};
    W -- Yes --> X[Update max_similarity, best_match_word];
    W -- No --> U; // Continue loop
    X --> U; // Continue loop (after update)
    U -- End Loop --> Y[Output: Best Match Word for Analogy and Similarity Score];
    Y --> D; // Back to main loop or End

    D --> Z[End Program];
