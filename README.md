### File modifications:      

    In file mcqa.py:        

    Line 183: majority_pred = vote_counts.most_common(1)["Write Your Code Here"]["Write Your Code Here"] -> majority_pred = vote_counts.most_common(1)[0][0]        

    In file modeling_llama.py:

    Line 287, 288: 
    self.up_proj = nn.Linear("Write Your Code Here", self.intermediate_size, bias=config.mlp_bias)
    self.down_proj = nn.Linear(self.intermediate_size, "Write Your Code Here", bias=config.mlp_bias)  
    -> 
    self.up_proj = nn.Linear(self.hidden_size, self.intermediate_size, bias=config.mlp_bias)     
    self.down_proj = nn.Linear(self.intermediate_size, self.hidden_size, bias=config.mlp_bias)     

    Line 356, 357, 358:
    self.q_proj = nn.Linear("Write Your Code Here", self.num_heads * self.head_dim, bias=config.attention_bias)
    self.k_proj = nn.Linear("Write Your Code Here", self.num_key_value_heads * self.head_dim, bias=config.attention_bias)
    self.v_proj = nn.Linear("Write Your Code Here", self.num_key_value_heads * self.head_dim, bias=config.attention_bias)
    ->
    self.q_proj = nn.Linear(self.hidden_size, self.num_heads * self.head_dim, bias=config.attention_bias)
    self.k_proj = nn.Linear(self.hidden_size, self.num_key_value_heads * self.head_dim, bias=config.attention_bias)
    self.v_proj = nn.Linear(self.hidden_size, self.num_key_value_heads * self.head_dim, bias=config.attention_bias)    

    Line 424: attn_weights = torch.matmul("Write Your Code Here", "Write Your Code Here") / math.sqrt(self.head_dim) -> attn_weights = torch.matmul(query_states, key_states) / math.sqrt(self.head_dim)

    Line 745: hidden_states = "Write Your Code Here" + hidden_states -> hidden_states = residual + hidden_states

 
        
        
    