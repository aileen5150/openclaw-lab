# Best Shopping-Category Personal Task

```
POST /api/help/request
Content-Type: application/json

{
  "request_id": "shp-2024-78432",
  "category": "electronics",
  "subcategory": "wireless-earbuds",
  "title": "Best wireless earbuds for serious runners",
  "user_context": {
    "primary_use": "running",
    "budget_range": "$100-$250",
    "dealbreaker_features": ["falling out during runs", "poor battery life", "sweat damage"]
  },
  "detailed_requirements": {
    "must_have": [
      "IPX5+ water/sweat resistance",
      "7+ hours battery life per charge",
      "Secure fit for pavement running at 7-9 min/mile pace",
      "Background noise awareness mode for traffic safety",
      "Stable Bluetooth 5.0+ connection"
    ],
    "nice_to_have": [
      "Heart rate monitoring",
      "GPS pace/distance tracking",
      "Multipoint pairing (switch between phone and laptop)",
      "Wireless charging case"
    ],
    "comparison_candidates": [
      "Jabra Elite 8 Active",
      "Sony WF-SP800N",
      "Jaybird Vista 2",
      "Powerbeats Pro",
      "Samsung Galaxy Buds2 Pro"
    ]
  },
  "research_priority": [
    "Fit security during high-impact movement (user reviews mentioning workouts)",
    "Sweat/moisture durability over 6+ months of use",
    "Sound isolation vs. ambient awareness balance",
    "Real-world battery performance vs. manufacturer claims",
    "Price trends and whether $180-$230 is the sweet spot or if cheaper alternatives exist"
  ],
  "format_preference": "detailed comparison table with performance ratings, specific user review quotes, current pricing with discount alerts, and clear recommendation with reasoning"
}
```

**Response:**

```json
{
  "status": "accepted",
  "request_id": "shp-2024-78432",
  "estimated_completion": "2-3 hours",
  "bonus_awarded": "$0.05",
  "priority_queue": "high"
}
```