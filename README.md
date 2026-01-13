-- 신청 테이블
CREATE TABLE submissions (
  id BIGSERIAL PRIMARY KEY,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  type TEXT NOT NULL,
  name TEXT NOT NULL,
  phone TEXT NOT NULL,
  biz_num TEXT,
  region TEXT,
  message TEXT,
  status TEXT DEFAULT '신규'
);

-- 팝업 테이블
CREATE TABLE popups (
  id BIGSERIAL PRIMARY KEY,
  title TEXT NOT NULL,
  icon TEXT DEFAULT '📢',
  description TEXT,
  btn_text TEXT DEFAULT '자세히 보기 →',
  btn_link TEXT DEFAULT '#contact',
  image_url TEXT,
  active BOOLEAN DEFAULT true
);

-- 공지 테이블
CREATE TABLE notice (
  id BIGSERIAL PRIMARY KEY,
  text TEXT,
  show BOOLEAN DEFAULT true,
  color TEXT DEFAULT 'mint'
);

-- 설정 테이블
CREATE TABLE settings (
  id BIGSERIAL PRIMARY KEY,
  phone TEXT DEFAULT '1660-3543',
  email TEXT DEFAULT 'pro_5211@naver.com',
  kakao TEXT,
  hours TEXT DEFAULT '09:00 ~ 익일 08:00'
);

-- 어드민 테이블
CREATE TABLE admin (
  id BIGSERIAL PRIMARY KEY,
  username TEXT NOT NULL,
  password TEXT NOT NULL
);

-- 기본 데이터 추가
INSERT INTO admin (username, password) VALUES ('admin', 'teambro2025');
INSERT INTO settings (phone) VALUES ('1660-3543');
INSERT INTO notice (text) VALUES ('📢 전국 협력사 대모집! 지금 바로 신청하세요!');

-- RLS 비활성화 (테스트용)
ALTER TABLE submissions ENABLE ROW LEVEL SECURITY;
ALTER TABLE popups ENABLE ROW LEVEL SECURITY;
ALTER TABLE notice ENABLE ROW LEVEL SECURITY;
ALTER TABLE settings ENABLE ROW LEVEL SECURITY;
ALTER TABLE admin ENABLE ROW LEVEL SECURITY;

-- 모든 접근 허용 정책
CREATE POLICY "Allow all" ON submissions FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "Allow all" ON popups FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "Allow all" ON notice FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "Allow all" ON settings FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "Allow all" ON admin FOR ALL USING (true) WITH CHECK (true);
