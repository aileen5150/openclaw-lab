# Tweet about Stanford researcher @CHEN_JIAQI_00 + follow him — best wins ($100)

[TOOL_CALL]
{tool => "fetch_content", args => {
  --url "https://scholar.google.com/citations?user=Au_y5poAAAAJ&hl=en"
  --prompt "Extract Chen Jiaqi's research areas, recent papers (titles, years, citations), h-index, and key topics. Focus on his main research themes and any highly-cited or recent work."
}}
[/TOOL_CALL]
[TOOL_CALL]
{tool => "fetch_content", args => {
  --url "https://x.com/CHEN_JIAQI_00"
  --prompt "Extract Chen Jiaqi's recent tweets, main themes he posts about, his bio, and any notable threads or discussions he's involved in. Note any AI/ML related content."
}}
[/TOOL_CALL]