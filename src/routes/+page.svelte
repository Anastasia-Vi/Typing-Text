<script>
    import { Card, Grid, Row } from "$lib/ui/Grid";
    
  </script>
   <div class="container">
    <Row>
      <Grid>
        <Card col={6}>
                <!-- Score blocks -->
                    <div class="score-block">
                        <h3>Player 1</h3>
                        <div class="score">0</div>
                    </div>
                    <Card col={6}>
                        <div class="score-block">
                            <h3>Player 2</h3>
                            <div class="score">0</div>
                        </div>
                    </Card>
            
                <!-- Game table -->
                <div class="table">
                    <!-- Cards will be placed here -->
                    <div class="cards-grid">
                        <!-- 36 cards -->
                        <div class="card"></div>
                        <div class="card"></div>
                        <!-- ... repeat for all 36 cards ... -->
                    </div>
                </div>
        </Card>
      </Grid>
    </Row>
</div>


<style>
.container {
    background-color: #2c3e50;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
    
    .game-container {
        width: 90%;
        max-width: 1200px;
    }
    
    /* Score blocks styling */
    .score-container {
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
    }
    
    .score-block {
        background-color: #34495e;
        padding: 15px;
        border-radius: 10px;
        color: white;
        text-align: center;
        width: 150px;
    }
    
    .score {
        font-size: 24px;
        font-weight: bold;
        margin-top: 10px;
    }
    
    /* Table styling */
    .table {
        background-color: #27ae60;
        border-radius: 20px;
        padding: 20px;
        box-shadow: 0 0 20px rgba(0,0,0,0.3);
    }
    
    /* Cards grid */
    .cards-grid {
        display: grid;
        grid-template-columns: repeat(9, 1fr);
        gap: 10px;
        padding: 20px;
    }
    
    /* Card styling */
    .card {
        background-color: white;
        border-radius: 8px;
        height: 100px;
        cursor: pointer;
        transition: transform 0.2s;
        box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    }
    
    .card:hover {
        transform: translateY(-5px);
    }
    
    /* Responsive design */
    @media (max-width: 1200px) {
        .cards-grid {
            grid-template-columns: repeat(6, 1fr);
        }
    }
    
    @media (max-width: 768px) {
        .cards-grid {
            grid-template-columns: repeat(4, 1fr);
        }
    }
    
    @media (max-width: 480px) {
        .cards-grid {
            grid-template-columns: repeat(3, 1fr);
        }
    }
</style>