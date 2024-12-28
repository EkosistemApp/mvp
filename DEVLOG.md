# EKOSISTEM.APP DEVELOPMENT LOG

### Oturum Devam: 2024-12-28 20:10 (GMT+2)

9. [Güncelleme] Proje Dizin Yapısı Revize Ediliyor
   ```
   ekosistem-app/
   ├── src/
   │   ├── app/
   │   │   ├── admin/        # Admin Panel Routes
   │   │   │   ├── auth/
   │   │   │   │   └── login/
   │   │   │   ├── dashboard/
   │   │   │   ├── topics/
   │   │   │   ├── organizations/
   │   │   │   ├── community/
   │   │   │   ├── layout.tsx
   │   │   │   └── page.tsx
   │   │   ├── (auth)/      # User Platform Auth
   │   │   │   ├── login/
   │   │   │   └── invite/
   │   │   ├── (platform)/  # User Platform Routes
   │   │   │   ├── feed/
   │   │   │   ├── profile/
   │   │   │   ├── messages/
   │   │   │   └── organizations/
   │   │   ├── layout.tsx
   │   │   └── page.tsx
   │   ├── components/
   │   │   ├── admin/       # Admin Components
   │   │   │   ├── ui/
   │   │   │   └── shared/
   │   │   ├── platform/    # Platform Components
   │   │   │   ├── ui/
   │   │   │   └── shared/
   │   │   └── common/      # Common Components
   │   ├── lib/
   │   │   ├── supabase/
   │   │   │   ├── admin.ts
   │   │   │   └── client.ts
   │   │   └── utils/
   │   └── types/
   ├── public/
   │   ├── admin/
   │   └── platform/
   └── .env.local
   ```

10. [Aksiyon] Supabase Proje Kurulumu ve Rol Ayrımı
    - İki ayrı auth konfigürasyonu yapılacak:
      1. Admin Panel Auth (email/password)
      2. Platform Auth (davetiye sistemi)
    
    - Database Rol ve Politikaları:
    ```sql
    -- Admin roles
    CREATE ROLE admin_role;
    GRANT ALL ON ALL TABLES IN SCHEMA public TO admin_role;
    
    -- Platform user roles
    CREATE ROLE platform_user;
    GRANT SELECT, INSERT, UPDATE ON [specific_tables] TO platform_user;
    ```

11. [Aksiyon] Environment Variables Genişletiliyor
    ```env
    # Admin Panel Environment Variables
    NEXT_PUBLIC_SUPABASE_URL=
    NEXT_PUBLIC_SUPABASE_ADMIN_ANON_KEY=
    SUPABASE_ADMIN_SERVICE_ROLE_KEY=
    ADMIN_PANEL_URL=

    # Platform Environment Variables
    NEXT_PUBLIC_SUPABASE_PLATFORM_ANON_KEY=
    SUPABASE_PLATFORM_SERVICE_ROLE_KEY=
    PLATFORM_URL=
    ```

12. [Planlama] İlk Aşama Geliştirme Sırası:
    1. Admin Panel Auth ve Dashboard
    2. Admin Topic Management
    3. Platform Auth (Davetiye Sistemi)
    4. Platform Feed Yapısı 

### Oturum Devam: 2024-12-28 20:14 (GMT+2)

16. [Güncelleme] Çalışma Modu Değişikliği
    - Agent moduna geçildi
    - Dosya değişiklikleri doğrudan yapılacak
    - Önemli karar noktalarında onay alınacak
    - Tüm değişiklikler log'lara kaydedilecek

17. [Başlıyor] Admin Panel Auth Sistemi Kurulumu
    - Dosya yapısı oluşturulacak
    - Auth komponenetleri hazırlanacak
    - Middleware yapılandırılacak 