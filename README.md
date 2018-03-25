# FirebaseChatAppLBTA
Collection, firebase, animation, TableView in code

(1) Login and Signup using same textfied in code.
    - constraints get set for hide name in login that was available in register
    - upload image and upload video using ImagePickerView
    - get image thumbnail of video 
       
        fileprivate func thumbnailImageForFileUrl(_ fileUrl: URL) -> UIImage? {
        let asset = AVAsset(url: fileUrl)
        let imageGenerator = AVAssetImageGenerator(asset: asset)
        
        do {
        
            let thumbnailCGImage = try imageGenerator.copyCGImage(at: CMTimeMake(1, 60), actualTime: nil)
            return UIImage(cgImage: thumbnailCGImage)
            
        } catch let err {
            print(err)
        }
        
        return nil
        }
    
    - perfect example of ios 9 constraints using NSAnchor of NSlayout for loginview
    - collection view of chat layout done in coding using two way
    - UICollectionview have called property called inputAccesoryView
         when scrolling happens and this property will be set
          - collectionView?.keyboardDismissMode = .interactive
      
       // this inputContainerView contains TextField, Send Button, image upload button for chat APP to send message
       override var inputAccessoryView: UIView? {
        get {
            return inputContainerView
           }
        }
     
     - get height of textview of dynamic text using this func. we need to just pass String. it returns CGRect
         fileprivate func estimateFrameForText(_ text: String) -> CGRect {
          let size = CGSize(width: 200, height: 1000)
          let options = NSStringDrawingOptions.usesFontLeading.union(.usesLineFragmentOrigin)
          return NSString(string: text).boundingRect(with: size, options: options, attributes: [NSFontAttributeName:     UIFont.systemFont(ofSize: 16)], context: nil)
         }
      - In chat Application Uicollection cell containg Text, image and video for chat VC they all are put in bubbleVIew.
        and setting dynamic height and width for it. check that code.. go inside
      
      - Image caching using UIImageVIew Extension
      
            import UIKit
            // NScaching for imageview image data
            let imageCache = NSCache<AnyObject, AnyObject>()
            extension UIImageView {
   
            func loadImageUsingCacheWithUrlString(_ urlString: String) {
        
                self.image = nil

                //check cache for image first
                if let cachedImage = imageCache.object(forKey: urlString as AnyObject) as? UIImage {
                    self.image = cachedImage
                    return
                }

                //otherwise fire off a new download
                let url = URL(string: urlString)
                URLSession.shared.dataTask(with: url!, completionHandler: { (data, response, error) in

                    //download hit an error so lets return out
                    if error != nil {
                        print(error ?? "")
                        return
                    }

                    DispatchQueue.main.async(execute: {

                        if let downloadedImage = UIImage(data: data!) {
                            imageCache.setObject(downloadedImage, forKey: urlString as AnyObject)

                            self.image = downloadedImage
                        }
                    })

                    }).resume()
                  }

                }
      
      
      
      
