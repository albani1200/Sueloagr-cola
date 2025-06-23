# Sueloagricola

## Código para la creación de un gráfico de densidad microbiana a partir de datos reales

```library(ggplot2)
library(dplyr)
datos <- data.frame(
    Sitio = c("S1", "S2", "S3", "S4", "S5", "S6"),
    log10_UFC = c(6.928, 6.3134, 4.641, 6.112901, 4.694558, 6.023),
    stringsAsFactors = FALSE
) %>%
    # 
    arrange(desc(log10_UFC)) %>%
    mutate(Sitio = factor(Sitio, levels = Sitio))


colores_deseados <- c("#f96405", "#efbc94", "#23ac74", 
                            "#56995a", "#d4a8c4", "#5e5e5e")


grafico <- ggplot(datos, aes(x = Sitio, y = log10_UFC, fill = Sitio)) +
    geom_col(width = 0.7, color = "black", alpha = 0.8) +
    geom_text(aes(label = round(log10_UFC, 3)),
              vjust = -0.5, size = 5, fontface = "bold", color = "black") +
    scale_fill_manual(values = colores_personalizados) +
    labs(
        title = "DENSIDAD MICROBIANA EN SITIOS DEL CAMPUS",
        subtitle = "Valores de log10 UFC/g (promedio de 6 experimentos)",
        x = "Sitios de muestreo",
        y = "log10 UFC/g",
        fill = "Sitio"
    ) +
    theme_minimal(base_size = 14) +
    theme(
        plot.title = element_text(hjust = 0.5, face = "bold", size = 16),
        plot.subtitle = element_text(hjust = 0.5, size = 12),
        axis.text.x = element_text(angle = 45, hjust = 1, face = "bold"),
        axis.title = element_text(face = "bold"),
        panel.grid.major.x = element_blank(),
        legend.position = "none",
        plot.margin = unit(c(1, 1, 2, 1), "cm")
    ) +
    scale_y_continuous(limits = c(0, 8),  # Eje Y desde 0 hasta 8
                       breaks = seq(0, 8, by = 1),  # Marcas cada 1 unidad
                       expand = expansion(mult = c(0, 0.1)))

print(grafico)

ggsave("densidad_microbiana_ejeY_hasta8.png", 
       plot = grafico, 
       width = 10, 
       height = 7, 
       dpi = 300, ```

       
