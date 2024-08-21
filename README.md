# WS2812_rainbow
```
void calculate_RGB(float angle, uint8_t* r, uint8_t* g, uint8_t* b) {
    float normalized_angle = angle / 360.0; // 각도를 0에서 1 사이 값으로 정규화

    // 각도에 따라 RGB 값을 계산
    if (normalized_angle < 1.0 / 3.0) { // 0도 ~ 120도: 빨강에서 초록으로
        *r = 255 * (1 - 3 * normalized_angle);//감소 
        *g = 255 * (3 * normalized_angle);//증가 
        *b = 0;
    } else if (normalized_angle < 2.0 / 3.0) { // 120도 ~ 240도: 초록에서 파랑으로
        *r = 0;
        *g = 255 * (1 - 3 * (normalized_angle - 1.0 / 3.0));//감소
        *b = 255 * (3 * (normalized_angle - 1.0 / 3.0));//증가
    } else { // 240도 ~ 360도: 파랑에서 빨강으로
        *r = 255 * (3 * (normalized_angle - 2.0 / 3.0));//증가
        *g = 0;
        *b = 255 * (1 - 3 * (normalized_angle - 2.0 / 3.0));//감소
    }
}
```
```
void rainbow_cycle(uint8_t *scroll_led_buf, int num_leds) {
    for (int i = 0; i < num_leds; ++i) {
		
        float ratio = (float)i / (float)(num_leds - 1); // LED 위치 비율 계산
        float angle = ratio * 360.0; // 각도 계산
        uint8_t R_Value, G_Value, B_Value;
        calculate_RGB(angle, &R_Value, &G_Value, &B_Value); // 각도에 따른 RGB 값 계산
        int start_idx = i * 3;
        scroll_led_buf[start_idx] = G_Value; // 초록색 설정
        scroll_led_buf[start_idx + 1] = R_Value; // 빨강색 설정
        scroll_led_buf[start_idx + 2] = B_Value; // 파랑색 설정
        
    }
}
```
