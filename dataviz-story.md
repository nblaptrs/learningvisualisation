class: middle

 # Tell a different story

---

## Free scales

.panelset[

.panel[.panel-name[Plot]
```{r ref.label="free-scales", echo = FALSE, fig.asp = 0.45, out.width = "90%"}
```
]

.panel[.panel-name[Code]

```{r free-scales, fig.show = "hide"}
ggplot(brexit, aes(y = opinion, fill = opinion)) +
  geom_bar() +
  facet_wrap(~region, nrow = 1, labeller = label_wrap_gen(width = 12),
             scales = "free_x") + #<<
  guides(fill = FALSE) +
  labs(title = "Was Britain right/wrong to vote to leave EU?",
       subtitle = "YouGov Survey Results, 2-3 September 2019",
       caption = "Source: bit.ly/2lCJZVg",
       x = NULL, y = NULL) +
  scale_fill_manual(values = c("Wrong" = "#ef8a62",
                               "Right" = "#67a9cf",
                               "Don't know" = "gray")) +
  theme_minimal()
```
]

]

---

## Comparing proportions across facets

.panelset[

.panel[.panel-name[Plot]
```{r ref.label="compare-props-facets", echo = FALSE, fig.asp = 0.45, out.width = "90%"}
```
]

.panel[.panel-name[Calculate]
```{r}
brexit %>% 
  count(region, opinion) %>% 
  group_by(region) %>% 
  mutate(opinion_prop = n / sum(n))
```
]

.panel[.panel-name[Code]

```{r compare-props-facets, fig.show = "hide"}
brexit %>% 
  count(region, opinion) %>% 
  group_by(region) %>% 
  mutate(opinion_prop = n / sum(n)) %>% 
  ggplot(aes(y = opinion, x = opinion_prop, fill = opinion)) + #<<
  geom_col() + #<<
  facet_wrap(~region, nrow = 1, labeller = label_wrap_gen(width = 12)) +
  guides(fill = FALSE) +
  labs(title = "Was Britain right/wrong to vote to leave EU?",
       subtitle = "YouGov Survey Results, 2-3 September 2019",
       caption = "Source: bit.ly/2lCJZVg",
       x = NULL, y = NULL) +
  scale_fill_manual(values = c("Wrong" = "#ef8a62",
                               "Right" = "#67a9cf",
                               "Don't know" = "gray")) +
  scale_x_continuous(labels = label_percent()) + #<<
  theme_minimal()
```
]

]

---

## Comparing proportions across bars

.panelset[

.panel[.panel-name[Plot]
```{r ref.label="compare-props-bars", echo = FALSE, fig.asp = 0.45, out.width = "90%"}
```
]

.panel[.panel-name[Code]

```{r compare-props-bars, fig.show = "hide"}
brexit %>%
  count(region, opinion) %>%
  group_by(region) %>%
  mutate(opinion_prop = n / sum(n)) %>%
  ggplot(aes(y = fct_rev(region), x = opinion_prop, fill = opinion)) + 
  geom_col(position = "dodge") + #<<
  labs(title = "Was Britain right/wrong to vote to leave EU?",
       subtitle = "YouGov Survey Results, 2-3 September 2019",
       caption = "Source: bit.ly/2lCJZVg",
       x = NULL, y = NULL) +
  scale_fill_manual(values = c("Wrong" = "#ef8a62",
                               "Right" = "#67a9cf",
                               "Don't know" = "gray")) +
  guides(fill = guide_legend(reverse = TRUE)) + #<<
  scale_x_continuous(labels = label_percent()) +
  theme_minimal()
```
]

]
