<details {% if open %} open {% endif %} >
<summary>{{ summary }}</summary>
{{ body | markdown(inline=true) }}
</details>
